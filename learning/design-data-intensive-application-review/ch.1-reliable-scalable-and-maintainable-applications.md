---
description: >-
  Introduces the terminology and approach that is going to use throughout this
  book. It examines the words like reliability, scalability, and
  maintainability.
---

# Ch.1 Reliable, Scalable, and Maintainable Applications

Three concerns that are important in most software systems:

* Reliability: Keep systems work correctly, even faults occur(hardware, user mistake)
  * Fault: One component of the system deviating from its spec
  * Failure: The whole system stops providing the required service to the user
  * Fault-tolerant is to cope with certain type of fault to prevent from failure
  * Way to increase reliability
    * Redundant hardware
    * Sandbox environment / Testing at every stage
    * Quick Rollback / recovery
    * Monitor / Troubleshooting



* Scalability: The ability to cope with increased load
  * How to define load? (e.g. Twitter's Post Tweet, Home Timeline)
    * For most people posting a tweet, Twitter use **fan-out** algorithm, sending the post to their follower's home timeline cache because the amount is small)
    * For celebrity, their tweet will be inserted to global collection of tweets, and when users request their timeline, servers look up all people they followed and merge those tweet while sorting by time.
  *   Performance metrics (to measure how well the system handle data load)

      * Throughput: Number of records the system can process per second
      * Response Time (Median): 50% waits longer, and 50% waits shorter. It is approximately equals to latency + network delay
      * Tail latency amplification could affect UX and cause more cost than it seems to be, thus 99% response time(p99) also matters.
      * It takes just a single slow backend request to slow down the entire end-user request.
      * An architecture that scales well for a particular application is **built around** **assumptions** of **which operations will be common** **and rare.** Could be volume of read, volume of write, volume of data to store, complexity of data, response time requirement, or the mix of above.


* Maintainability: Includes Operability(Easy for Operations), Simplicity(Easy for Management), and Evolvability(Easy for Change)
  * Good abstractions can help reduce complexity and make the system easier to modify and adapt for new use cases. (e.g. SQL hides complex on-disk and in-memory data structures)



