---
description: Overview of 3 main problem of cache system
---

# Cache

### Cache avalanche:&#x20;

> A large number of keys set the same expiration time, resulting in the cache at the same time all failed, resulting in a large amount of instantaneous db requests, pressure surges, causing avalanches.

Solution:&#x20;

Set the expiration time for the cache by adding a random value time, so that each key's expiration time is distributed, and will not fail at the same time.

### Cache penetration:&#x20;

> Hacker attempt to make request with keys that don't exist in cache and database. It's eventually an invalid request which if not handle well will keep returning null and crash the database

Solution:&#x20;

1. If there is no data for the key in DB, just return an empty result and cache it for a short period of time(Don't set a long expiration time)
2. Using Bloom filter. [Bloom filter](https://en.wikipedia.org/wiki/Bloom\_filter) is similar to hbase set which can be used to check whether a key exists in the data set. If the key exists, go to the cache layer or DB layer, if it doesn't exists in the data set, then just return.

### Cache breakdown:&#x20;

> A frequent cache expires at the time when lots of request comes in and paralize the database

Solution:

Have a good cache eviction policy, for example using a Least Recently Used (LRU) algorithm, and monitoring the cache usage to identify these issues as soon as possible.



### Reference

[Seeing through hardware counters: a journey to threefold performance increase](https://netflixtechblog.com/seeing-through-hardware-counters-a-journey-to-threefold-performance-increase-2721924a2822)

[Cache breakdown, Cache penetration, cache avalanche](https://topic.alibabacloud.com/a/cache-breakdown-cache-penetration-cache-avalanche\_8\_8\_31058782.html)

[14 缓存策略：面试中如何回答缓存穿透、雪崩等问题？](https://www.youtube.com/watch?v=cLzUC38BR-c)

[Cache invalidation really is one of the hardest problems in computer science](https://surfingcomplexity.blog/2022/11/25/cache-invalidation-really-is-one-of-the-hardest-things-in-computer-science/)



\


\


\


