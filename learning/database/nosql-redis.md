---
description: >-
  Redis stands for Remote Dictionary Server. It is a key-value Database backed
  by hash table.
---

# \[NoSQL] Redis

### What is Redis?

* Key-value database
* In-memory, persistent on disk
* Provides support for atomic operations on complex data types
* Supported by numerous programming languages

### Why Redis is fast

* Redis store data In-memory, which makes retrieval faster than in disk like traditional database
* Redis uses Hash table to achieve lots of operation in O(1) time
* Redis uses a simple, single-threaded event loop for handling client connections, which allows it to handle a large number of requests with minimal overhead (such as memory, CPU, network bandwidth)

### Typical Redis Interview Question

_Q: Is Redis single-thread or multi-thread?_

A: Redis is single-thread, so you can only process one command at a time. However, Redis can handle multiple client connections simultaneously(with multiplexing mechanism) and it can perform multiple operations in parallel.&#x20;

_Q: What is Redis Cluster_

A: Redis Cluster allows it to scale horizontally by sharding data across multiple nodes. Each node in the cluster runs a Redis instance, which is single-threaded, but the cluster as a whole can handle a much larger amount of data and requests.

_Q: How Redis persist its data_

A: Within Redis, there are two different ways of persisting data to disk.&#x20;

1. _AOF(append-only file): I_t copies incoming write commands to **disk** as they happen. The type of Redis AOF is postlog, all command will be written **after** the operation. It prevents blockages in write commands and logs invalid commands, but AOF can be slow in data recovery.
2. _Snapshotting: It_ writes data exist at one moment into **disk** to solve AOF slow recovery problem because you just read data from disk instead of repeating previous commands.&#x20;
3. _Hybrid_: Snapshot first and log write commands during snapshot

Q: _How Redis achieve high-availability_

A: There're 3 main mechanism to help Redis achieve high-availability

1.  Redis Cluster

    Redis Cluster is a method of horizontally scaling by dividing the keyspace across multiple Redis nodes. Each node runs a single-threaded Redis instance and is responsible for a subset of the total keyspace, called hash slots. Data is distributed among the hash slots using a sharding algorithm, allowing for efficient horizontal scaling.


2.  Primary-Secondary replication

    The primary database receives all write operations and propagates them to the secondary databases, which receive a copy of the data. This allows for read operations to be performed on the secondary databases, reducing the load on the primary and providing a way to scale read operations. In addition, the secondary databases can take over as primary if the original primary goes down. This allows for a failover with minimal data loss and downtime.


3.  Redis Sentinel

    Redis Sentinel is a service that provides automatic failover and other features to ensure high availability of Redis instances. It works by monitoring Redis masters and maintaining a configuration of their slaves. Sentinels can detect when a master is down and promote one of the slaves to take its place, thus reducing the impact of a failure and providing a fast recovery.

### When to use Key-Value Databases&#x20;

* Web-session data&#x20;
* Shopping cart data
* User profiles&#x20;

### When NOT to use Key-Value Databases&#x20;

* When you want to access data by value, not key
* When you want to describe complex relationships between (key, value) pairs
* When you will be frequently operating on multiple keys at the same time

### Redis syntax

| Syntax                               | Example                           | Effect                                                                  |
| ------------------------------------ | --------------------------------- | ----------------------------------------------------------------------- |
| `GET key`                            | `GET user:1`                      | retrieve the value of the key "user:1".                                 |
| `SET key value`                      | `SET user:1 "John Smith"`         | set the value of the key "user:1" to "John Smith".                      |
| `EXPIRE key seconds`                 | `EXPIRE user:1 3600`              | set a TTL of 1 hour for the key "user:1".                               |
| `LPUSH key value`                    | `LPUSH messages "Hello"`          | add "Hello" to the beginning of the list "messages".                    |
| `RPUSH key value`                    | `RPUSH messages "World"`          | add "World" to the end of the list "messages".                          |
| `LTRIM key start stop`               | `LTRIM messages 0 9`              | keep only the first 10 elements of the list "messages".                 |
| `HGET key field`                     | `HGET user:1 name`                | retrieve the value of the "name" field in the hash "user:1".            |
| `HSET key field value`               | `HSET user:1 age 30`              | set the value of the "age" field in the hash "user:1" to 30.            |
| `SADD key value`                     | `SADD online_users "user:1"`      | add "user:1" to the set "online\_users".                                |
| `SMEMBERS key`                       | `SMEMBERS online_users`           | retrieve all the members of the set "online\_users".                    |
| `DEL key`                            | `DEL user:1`                      | delete the key "user:1" and its associated value.                       |
| `INCR key`                           | `INCR page_view`                  | increase the value of "page\_view" by 1.                                |
| `ZADD key score value`               | `ZADD leaderboard 1000 "user:1"`  | add "user:1" to the "leaderboard" set with a score of 1000.             |
| `ZRANGE key start stop [WITHSCORES]` | `ZRANGE leaderboard 0 -1`         | return all elements in the leaderboard set.                             |
| `ZCOUNT key min max`                 | `ZCOUNT leaderboard 500 1000`     | return elements with score between \[500, 1000] in the leaderboard set. |
| `FLUSHDB`                            | `FLUSHD`                          | Remove all the keys of all the existing database                        |
| `PERSIST key`                        | `PERSIST key`                     | Remove the expiration from a key.                                       |

\


### Reference

[13 缓存原理：应对面试你要掌握 Redis 哪些原理？](https://www.youtube.com/watch?v=nrgATM0yPO8)

[14 缓存策略：面试中如何回答缓存穿透、雪崩等问题？](https://www.youtube.com/watch?v=cLzUC38BR-c)

[Chapter 4. Keeping data safe and ensuring performance](https://livebook.manning.com/book/redis-in-action/chapter-4/17)



