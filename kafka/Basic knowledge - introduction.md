What is it?
Kafka is a distributed event streaming platform

event == record == message
## topic, partition, offset, broker

**Topic**: stream of data
Just like SQL table, topic <=> table, message <=> row of data

**Kafka Cluster** là nhiều server tập trung lại thành một cụm làm việc với nhau: multi-brokers (multi-servers), Kafka server == Kafka broker

**Brokers** chịu trách nhiệm cho việc lưu trữ, đọc, ghi dữ liệu

**Message** được lưu tại offset của partition, partition được lưu ở topic, topic được lưu trữ trên file, trên disk, và tất cả đều được lưu trữ trên server.

các topic được chia đều cho các broker (partition) và được nhân bản (replica) để đảm bảo tính an toàn của dữ liệu

## send  and receive message 

### Producer
publish an event into specific topic
Connect to kafka brokers through TCP

### Consumer
Subscribe one or more kafka topics
Connect to kafka brokers through TCP
Consumers work in a consumer group


### Consumer group

