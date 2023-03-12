---
description: >-
  Map is a feature to  to transform the data emitted by an Observable into a new
  format. It is widely used as an intermediate operator in a pipeline of
  Observable operators to transform data in flight.
---

# \[RxJS] map vs. switchMap, mergeMap vs. exhauseMap vs. concatMap

There're 4 types of Map in RxJS, and each of them shines at different use case. Here's the table help you comparing them at one place



| Operator     | Description                                                                                                                                                                               | Use Case                                                                                                                                                                               |
| ------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `map`        | Applies a given function to each value emitted by the source Observable, and emits the resulting values as an output Observable.                                                          | Used for basic data transformation.                                                                                                                                                    |
| `switchMap`  | Projects each source value to an Observable which is merged in the output Observable, but when a new source value arrives, it cancels the previous subscription and starts a new one.     | Used when only the most recent inner Observable should be subscribed to, and previous Observables should be cancelled.                                                                 |
| `concatMap`  | Projects each source value to an Observable which is merged in the output Observable, in a serialized fashion waiting for each inner Observable to complete before moving on to the next. | Used when maintaining the order of emissions is important, such as in making sequential HTTP requests.                                                                                 |
| `exhaustMap` | Projects each source value to an Observable which is merged in the output Observable, but ignores new source values while an inner Observable is still executing.                         | Used when there are high-frequency events being emitted and only the first event needs to be processed, while the subsequent events should be ignored until the first event completes. |
| `mergeMap`   | Projects each source value to an Observable which is merged in the output Observable, and multiple inner Observables can be subscribed to at the same time.                               | Used when maintaining concurrency is important, such as in making parallel HTTP requests.                                                                                              |



### Example code&#x20;

#### Map: map required properties from data source

```typescript
users$ = from([
    { id: 1, name: 'sam', age: 12 },
    { id: 2, name: 'ariel', age: 22 },
  ]);
 
users$.map(({name, age}) => ({name, age})).subscribe((data) => console.log(data))
// {name: 'sam', age: 12}
// {name: 'ariel', age: 22} 
```

#### SwitchMap: Making API calls to get results based on input value. Using switchMap with debounceTime will only call API when user stop typing after an interval and cancel previous calls

```typescript
const searchEle = document.getElementById('search');
fromEvent(searchEle, 'keyup')
      .pipe(
        debounceTime(500),
        switchMap((event: any) => {
        // here could be making an asynchronous API call
          return of(event.target.value).pipe(delay(2000));
        })
      )
      .subscribe((data) => console.log(data));
```

#### MergeMap:  Making multiple API calls in parallel, and the sequence is not guarantee

```typescript
/**
 * Output: mergedMap: 30 \n mergedMap: 20 \n mergedMap: 10 \n
*/
    const merged$ = from([1, 2, 3]);

    merged$
      .pipe(mergeMap((input) => of(input * 10).pipe(delay((1 / input) * 1000))))
      .subscribe((value) => console.log('mergedMap: ', value)); 

```

#### ConcatMap: Executing each Observable in sequence. New Observable will only be executed when previous Observable is resolved.

```typescript
/**
     * Executing each Observable in sequence. New Observable will only be
     * executed when previous Observable is resolved.
     * Output: lisa -> arield -> sam. Totally 12 seconds
     */
    const concat$ = of(['lisa', 'ariel', 'sam']);

    concat$
      .pipe(
        concatMap((request: string[]) => {
          // map each string to an Observable that logs the string after a delay based on the length of the string
          return from(request).pipe(
            concatMap((str) => of(str).pipe(delay(str.length * 1000))),
            tap((str) =>
              console.log(
                `Concatmap: finished processing '${str}' after ${str.length}s`
              )
            )
          );
        })
      )
      .subscribe();
```

