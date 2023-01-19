# \[NoSQL] 4 type of NoSQL database schema

1. Key-Value / Redis, DynamoDB / Each key is associated with a single value.&#x20;
   1. 👌 No fixed schema, which allows for flexibility in data storage .
   2. 👌 Low latency due to the simple data model.
   3. 👎 Data size limitation. Redis store data in-memory, and DynamoDB has 400 kb limitation.
   4. 👎 Lack of the ability to perform complex data processing such as grouping
2. Document-oriented / MongoDB, CouchDB / Each document contains a set of key-value pairs.&#x20;
   1. Suitable when the data schema is semi-structured&#x20;
   2. MongoDB use BSON to store data while CouchDB use JSON
   3.
3. Column-family / Cassandra, Hbase / Each column can have multiple values.&#x20;
   1. Most similar to Relational Database&#x20;
   2. Suitable when the there're still high relation between data schema
4. Graph / Neo4j, OrientDB / Data is represented as nodes and edges.&#x20;

\
