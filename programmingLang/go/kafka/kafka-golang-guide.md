# Kafka in Go — Production Guide

Using [`segmentio/kafka-go`](https://github.com/segmentio/kafka-go) (pure Go, no cgo/librdkafka dependency — easier to build and deploy, especially in Docker/Alpine images).

```bash
go get github.com/segmentio/kafka-go
```

---

## 1. Producer

```go
package main

import (
	"context"
	"log"
	"time"

	"github.com/segmentio/kafka-go"
	"github.com/segmentio/kafka-go/snappy"
)

func NewProducer(brokers []string, topic string) *kafka.Writer {
	return &kafka.Writer{
		Addr:         kafka.TCP(brokers...),
		Topic:        topic,
		Balancer:     &kafka.Hash{}, // key-based partitioning for ordering guarantees
		RequiredAcks: kafka.RequireAll, // wait for all in-sync replicas (durability)
		Compression:  snappy.NewCompressionCodec().Code().Compression(),
		BatchTimeout: 10 * time.Millisecond, // small batching window for throughput
		BatchSize:    100,
		MaxAttempts:  5,           // retry on transient errors
		WriteTimeout: 10 * time.Second,
		ReadTimeout:  10 * time.Second,
		Async:        false, // sync writes = backpressure + error visibility
	}
}

func Produce(ctx context.Context, w *kafka.Writer, key, value []byte) error {
	msg := kafka.Message{
		Key:   key,
		Value: value,
		Time:  time.Now(),
	}

	ctx, cancel := context.WithTimeout(ctx, 5*time.Second)
	defer cancel()

	if err := w.WriteMessages(ctx, msg); err != nil {
		log.Printf("write failed: %v", err)
		return err
	}
	return nil
}

func main() {
	w := NewProducer([]string{"localhost:9092"}, "orders")
	defer w.Close()

	ctx := context.Background()
	if err := Produce(ctx, w, []byte("order-123"), []byte(`{"status":"created"}`)); err != nil {
		log.Fatal(err)
	}
}
```

---

## 2. Consumer (with graceful shutdown + manual commit)

```go
package main

import (
	"context"
	"log"
	"os"
	"os/signal"
	"syscall"
	"time"

	"github.com/segmentio/kafka-go"
)

func NewConsumer(brokers []string, topic, groupID string) *kafka.Reader {
	return kafka.NewReader(kafka.ReaderConfig{
		Brokers:        brokers,
		Topic:          topic,
		GroupID:        groupID, // enables consumer-group rebalancing
		MinBytes:       10e3,    // 10KB — wait for enough data to batch-fetch
		MaxBytes:       10e6,    // 10MB cap per fetch
		MaxWait:        1 * time.Second,
		CommitInterval: 0, // 0 = commit manually after successful processing (at-least-once)
		StartOffset:    kafka.LastOffset,
	})
}

func run(ctx context.Context, r *kafka.Reader) error {
	for {
		msg, err := r.FetchMessage(ctx) // does NOT auto-commit
		if err != nil {
			if ctx.Err() != nil {
				return nil // clean shutdown
			}
			log.Printf("fetch error: %v", err)
			continue
		}

		if err := process(msg); err != nil {
			// Don't commit — message will be redelivered.
			// Route to DLQ after N retries (see below).
			log.Printf("process error, offset %d: %v", msg.Offset, err)
			continue
		}

		if err := r.CommitMessages(ctx, msg); err != nil {
			log.Printf("commit error: %v", err)
		}
	}
}

func process(msg kafka.Message) error {
	log.Printf("consumed key=%s value=%s partition=%d offset=%d",
		msg.Key, msg.Value, msg.Partition, msg.Offset)
	return nil
}

func main() {
	r := NewConsumer([]string{"localhost:9092"}, "orders", "order-processor")
	defer r.Close()

	ctx, stop := signal.NotifyContext(context.Background(), syscall.SIGINT, syscall.SIGTERM)
	defer stop()

	if err := run(ctx, r); err != nil {
		log.Fatal(err)
	}
	log.Println("consumer shut down cleanly")
}
```

---

## Production Best Practices

### Reliability
- **Idempotent producers matter more than retries.** With `RequiredAcks: RequireAll` and retries enabled, a network blip can cause duplicate writes. Use an idempotency key (e.g., order ID) in your message value/headers and de-dupe on the consumer side, or use transactional writes if you need exactly-once across topics.
- **Manual offset commits.** Never rely on `CommitInterval` auto-commit for anything you can't afford to lose — commit only after the message is durably processed (DB write succeeded, etc.).
- **Dead-letter queue (DLQ).** After N failed processing attempts, publish the message to a `<topic>.dlq` topic instead of blocking the partition forever. A single poison message with auto-retry-forever will stall your whole partition.
- **Idempotent consumers.** At-least-once delivery is the practical default — design `process()` to be safe to run twice (upserts, not inserts).

### Performance
- **Batch on the producer.** `BatchSize`/`BatchTimeout` trade a few ms of latency for much higher throughput — tune based on your latency budget.
- **Compression.** `snappy` or `zstd` cut network/storage cost significantly; zstd gives better ratios if CPU allows.
- **Partition count is a ceiling on consumer parallelism.** One consumer per partition max per group — under-provisioning partitions caps your scale-out.
- **Fetch sizing (`MinBytes`/`MaxBytes`/`MaxWait`).** Too small = many small fetches, too large = higher tail latency. Start with the defaults above and tune from metrics.

### Operations
- **Consumer groups for horizontal scaling** — same `GroupID` across instances gives you automatic partition rebalancing.
- **Monitor consumer lag** (`kafka-consumer-groups.sh` or Burrow/Prometheus exporters) — lag creeping up is the #1 early warning sign of a problem.
- **Graceful shutdown** — always drain in-flight messages and commit offsets before exiting (see `signal.NotifyContext` pattern above). Abrupt kills cause reprocessing storms on restart.
- **Schema management.** Use Avro/Protobuf with a schema registry (Confluent Schema Registry or similar) rather than raw JSON once you have more than one producer/consumer team — it prevents silent breaking changes.
- **Timeouts everywhere.** Set explicit `WriteTimeout`/`ReadTimeout`/context deadlines — a hung broker connection without timeouts will leak goroutines and stall shutdown.

### Observability
- Emit structured logs with `partition`, `offset`, `topic`, `key` on every produce/consume error.
- Track: produce latency, consumer lag per partition, error/retry rates, DLQ volume.
- Use `kafka.Writer.Stats()` / `kafka.Reader.Stats()` (both expose built-in metrics) and pipe into Prometheus.

### Security (production clusters)
- Use SASL/SCRAM or mTLS for broker auth — never plaintext in prod.
```go
dialer := &kafka.Dialer{
    Timeout:   10 * time.Second,
    DualStack: true,
    TLS:       &tls.Config{...},
    SASLMechanism: mechanism, // scram.Mechanism
}
```
- Scope ACLs per topic/consumer-group — don't run with a cluster-admin credential in application pods.

---

## Alternative: confluent-kafka-go

If you need exactly-once semantics (transactions), admin API depth, or are already standardized on librdkafka in a polyglot org, `confluent-kafka-go` (cgo wrapper around librdkafka) is the more feature-complete option — at the cost of cgo build complexity (static linking, cross-compilation friction). For most services, `segmentio/kafka-go` is the simpler, more "Go-native" choice.
