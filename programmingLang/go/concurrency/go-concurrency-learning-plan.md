# Go Concurrency — Learning Plan

A progressive, hands-on plan to take you from "I know basic Go" to "I can write and debug concurrent Go confidently." Built around four phases. Each phase has concepts to learn, something to build, and a way to check you actually understand it.

Pace it however suits you — roughly one phase per week is a comfortable rhythm, but compress or stretch as needed. The most important rule: **write code for every concept.** Concurrency bugs hide from people who only read about it.

**Assumed starting point:** comfortable with Go syntax, functions, structs, interfaces, slices/maps, and error handling. If channels and `go` are brand new to you, that's exactly what this plan covers.

---

## Phase 1 — Foundations & Goroutines

The goal here is intuition: what concurrency actually is, and how a goroutine differs from a thread.

**Concepts**
- Concurrency vs. parallelism (they are not the same thing — watch Rob Pike's talk below before anything else).
- Goroutines: launching with `go`, the main goroutine, why the program exits when `main` returns.
- The cost model: goroutines are cheap (a few KB of stack), so you can have thousands.
- A mental model of the scheduler (the G-M-P model) — just enough to understand that goroutines are multiplexed onto OS threads, not 1:1 with them.
- Goroutine *leaks*: what happens when a goroutine blocks forever and never gets cleaned up.

**Build**
- A program that launches N goroutines, each printing its ID, and correctly waits for all of them to finish before exiting (you'll do this with a channel first, then later with `WaitGroup`).

**Check yourself**
- Explain out loud why `go fmt.Println("hi")` in `main` might print nothing.
- Explain why concurrency can make a program faster even on a single core (hint: blocking I/O).

---

## Phase 2 — Channels & Select

Channels are how goroutines communicate. This is the heart of Go's "share memory by communicating" philosophy.

**Concepts**
- Unbuffered vs. buffered channels, and the blocking behavior of each.
- Sending, receiving, and the comma-ok receive (`v, ok := <-ch`).
- Closing channels: who closes, when, and why receiving from a closed channel returns the zero value.
- `range` over a channel.
- Directional channel types (`chan<-`, `<-chan`) for safer APIs.
- The `select` statement: waiting on multiple channels, the `default` case for non-blocking ops, and timeouts with `time.After`.
- Nil channels and why a `select` case on a nil channel blocks forever (a surprisingly useful trick).

**Build**
- A **pipeline**: a generator goroutine that produces numbers, a stage that squares them, and a final stage that prints them — all connected by channels.
- A worker that does a unit of work but respects a `done` channel so it can be told to stop.

**Check yourself**
- When does sending on a buffered channel block?
- Why is closing a channel from the receiver side a bug? Who *should* close it?

---

## Phase 3 — Synchronization & Context

Channels aren't always the right tool. Sometimes you just need to protect shared state or coordinate lifetimes.

**Concepts**
- The `sync` package: `WaitGroup` (waiting for goroutines), `Mutex` and `RWMutex` (protecting shared data), `Once` (one-time init), and a glance at `sync.Cond`.
- `sync/atomic` for simple lock-free counters and flags.
- The Go memory model at a high level: the "happens-before" relationship and why unsynchronized access to shared data is undefined behavior.
- The `context` package — this is essential for real-world Go: cancellation, deadlines, timeouts, and passing request-scoped values. Learn `context.WithCancel`, `WithTimeout`, and how to respect `ctx.Done()` in your goroutines.
- The race detector: run everything with `go run -race` and `go test -race`. Make this a habit now.

**Build**
- A concurrent counter that's incremented by many goroutines — first build it *wrong* (no synchronization), run it with `-race`, watch it fail, then fix it with both a `Mutex` and an atomic and compare.
- A function that does work but cancels cleanly when its `context` is cancelled or times out.

**Check yourself**
- When would you reach for a mutex instead of a channel? (Protecting a small piece of shared state usually favors a mutex.)
- What does the `-race` flag actually detect, and what can it miss?

---

## Phase 4 — Patterns & Production Concerns

Now you assemble the primitives into the patterns you'll actually use at work.

**Concepts & patterns**
- **Worker pools**: a fixed number of goroutines pulling jobs off a channel — the workhorse pattern for bounded parallelism.
- **Fan-out / fan-in**: distributing work across goroutines and merging results back.
- **Pipelines with cancellation**: chaining stages that all shut down cleanly.
- **Rate limiting** and **semaphores** (bounding concurrency with a buffered channel or `golang.org/x/sync/semaphore`).
- `golang.org/x/sync/errgroup` for running a group of goroutines and collecting the first error — you'll use this constantly.
- Common failure modes and how to avoid them: deadlocks, goroutine leaks, and sending on closed channels.

**Build a capstone**
- A **concurrent web crawler or scraper**: fetch a list of URLs with a bounded worker pool, respect a timeout via `context`, collect results and errors, and shut down cleanly. This single project exercises almost everything above.

**Check yourself**
- Limit your crawler to exactly 5 concurrent requests. How did you bound it?
- Kill the program mid-run with a cancelled context. Does it leak goroutines? Verify with `runtime.NumGoroutine()`.

---

## Core Resources

**Watch first**
- Rob Pike — *Concurrency is not Parallelism* (short talk, sets the right mental model).
- Rob Pike — *Go Concurrency Patterns* (the classic patterns talk).

**Read**
- The Go Tour — the concurrency section is the fastest interactive intro.
- *Go by Example* — concise runnable snippets for goroutines, channels, select, worker pools, etc.
- *The Go Programming Language* (Donovan & Kernighan), chapters 8–9 — excellent, rigorous coverage.
- *Concurrency in Go* by Katherine Cox-Buday — the dedicated, deep book on the subject. Worth it once the basics click.
- The Go Blog: *Go Concurrency Patterns: Pipelines and cancellation*, and *Advanced Go Concurrency Patterns*.

**Reference**
- The official Go Memory Model document (read once you've hit Phase 3).
- `pkg.go.dev` docs for `sync`, `sync/atomic`, `context`, and `golang.org/x/sync`.

---

## Habits That Matter More Than Any Resource

1. **Always run with `-race` during development.** Most concurrency bugs are invisible until this catches them.
2. **Every goroutine you start needs a clear exit path.** If you can't say how a goroutine ends, you've probably written a leak.
3. **Decide who owns each channel's close.** Senders close, receivers don't.
4. **Reach for the simplest tool.** A mutex around a map is often clearer than an elaborate channel dance.
5. **Build the broken version on purpose.** Seeing a deadlock or race happen teaches more than reading about it.
