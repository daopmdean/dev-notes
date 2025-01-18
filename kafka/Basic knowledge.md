
## topic, partition, offset, broker

Topic: stream of data
Just like SQL table, topic <=> table, message <=> row of data

Kafka Cluster là nhiều server tập trung lại thành một cụm làm việc với nhau: multi-brokers (multi-servers)

Message được lưu tại offset của partition, partition được lưu ở topic, topic được lưu trữ trên file, trên disk, và tất cả đều được lưu trữ trên server.

các topic được chia đều cho các broker (partition) và được nhân bản (replica) để đảm bảo tính an toàn của dữ liệu

## send  and receive message 

Producer
Consumer
Consumer group

