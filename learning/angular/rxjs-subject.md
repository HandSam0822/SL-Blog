---
description: >-
  Explore the four types of Subjects in RxJS in this article, which covers their
  functionality and use cases to guide developers in using these powerful tools.
---

# \[RxJS] Subject

There're 4 types of Subject in RxJS, Subject, BehaviorSubject,  ReplaySubject, and AsyncSubject. Each of them provide different but similar data stream solution.

| Subject Type      | Description                                                                                                          | Advantages                                                                                             | Disadvantages                                                                                        |
| ----------------- | -------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------- |
| `Subject`         | A simple subject that allows values to be pushed manually using `next()`.                                            | Easy to use and understand.                                                                            | Lacks some of the advanced features of the other types of Subjects.                                  |
| `BehaviorSubject` | A type of Subject that requires an initial value and replays the latest value or a default value to new subscribers. | Guarantees that new subscribers will always receive the most recent value.                             | Requires an initial value and can be confusing to use if not initialized properly.                   |
| `ReplaySubject`   | A type of Subject that records a specified number of values and replays them to new subscribers.                     | Allows new subscribers to receive a specified number of values, not just the most recent one.          | Requires specifying the number of values to replay and can use more memory than other Subject types. |
| `AsyncSubject`    | A type of Subject that only emits the last value it received, but only when it completes.                            | Guarantees that subscribers will always receive a value, even if the Observable completes immediately. | Can be confusing to use if the Observable never completes, since no value will be emitted.           |



