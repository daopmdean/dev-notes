# Index mongodb

[Manage Indexs](https://www.mongodb.com/docs/compass/current/indexes/)

[Create Index](https://www.mongodb.com/docs/manual/reference/method/db.collection.createIndex/)

```
db.getCollection("collection_name").createIndex({
  field_name_1: 1, field_name_2: -1
}, {background: true})
```
