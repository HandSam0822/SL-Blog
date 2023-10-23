---
description: Description of side effect
---

# \[RxJS] Functional Programming

### Functional Programming

Programming as a stream of data flow instead of objects.&#x20;

✅ Imperative (tell program to do **what** you want to achieve)&#x20;

❌ Declarative (Tell program **how** you want to achieve)

✅ Data processing and computation&#x20;

❌ I/O operation

No side effect. Predicable result.



### Side Effect

To verify whether the operation has side effect, we could ask ourself 2 questions

1. Do we always get the same result with the same input?
2. Does the function do anything **irrelevant to return value** such as modify global variables, change input parameters, console.log debugging message, etc.

#### Common operation with side effect

*   Sending http request

    Relying on external can't guarantee us to always get same output
*   Get user input & Query DOM element

    In some cases, getting user input and query DOM element can be used to change the state of the application, for example, to submit a form or to initiate an action. These inputs are considered "write" side effects, as they change the state of the application and can cause unpredictable changes in the behavior of the application.
*   console.log

    Doesn't contain **pure** **logic**

####

\






