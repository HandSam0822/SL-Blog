---
description: >-
  DynamoDB and MongoDB are both popular NoSQL databases that have their own
  strengths and weaknesses. Here's an overview:
---

# \[NoSQL] DynamoDB vs. MongoDB

|             | MongoDB                                                                                                                                                                                                                                                                                                                         | DynamoDB                                                                                                                                                                                                                                                                                                      |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Data Model  | document; stored in collections                                                                                                                                                                                                                                                                                                 |  key-value; stored table                                                                                                                                                                                                                                                                                      |
| Querying    | Supports more complex queries and aggregation operations                                                                                                                                                                                                                                                                        | Limited; Based on the primary key or secondary indexes                                                                                                                                                                                                                                                        |
| Consistency | MongoDB is **strongly consistent** by default as all read/writes go to the primary in a MongoDB replica set, scaled across multiple partitions (shards). If desired, consistency requirements for read operations can be relaxed by routing  requests only to secondary replicas that fall within acceptable consistency limits | <p>Supports <em><strong>eventually consistent</strong></em> and <em><strong>strongly consistent</strong></em> reads, but <em>strongly consistent reads</em>:</p><ul><li>Doesn't supported on global secondary indexes (<strong>GSI</strong>) and will use <strong>more throughput</strong> capacity</li></ul> |
| Cost        | Cheaper for large scale                                                                                                                                                                                                                                                                                                         | More variable                                                                                                                                                                                                                                                                                                 |

###

### Reference

[Comparing DynamoDB and MongoDB](https://www.mongodb.com/compare/mongodb-dynamodb)

[\[DynamoDB\] Read consistency](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/HowItWorks.ReadConsistency.html)

[\[DynamoDB\] AWS DynamoDB Tutorial For Beginners](https://www.youtube.com/watch?v=2k2GINpO308)

[\[MongoDB\] Data Modeling Introduction](https://www.mongodb.com/docs/v5.3/core/data-modeling-introduction/)

[\[MongoDB\] Read Isolation, Consistency, and Recency](https://www.mongodb.com/docs/v5.3/core/read-isolation-consistency-recency/)

\


