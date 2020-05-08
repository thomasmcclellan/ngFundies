##### 5/08/2020
# Observable Overview - Subscribing
An `Observable` instance begins publishing values only when someone subscribes to it.  You subscribe by calling the `subscribe()` method of the instance, passing an observer `object` to receive the notifications.

  > In order to show how subscribing works, we need to create a new `observable`.  There is a constructor that you use to create new instances, but for illustration, we can use some methods from the `RxJS` library that create simple `observables` of frequently used types:
  >   * `of(...items)`: Returns an `Observable` instance that synchronously delivers the values provided as arguments
  >   * `from(iterable)`: Converts its arguments to an `Observable` instance.  This method is commonly used to convert an `array` to an `Observable`

Here is an example of creating and subscribing to a simple `observable`, with an observer that logs the received message to the console:

```ts
// Create simple observable that emits three values
const myObservable = of(1, 2, 3);

// Create observer object
const myObserver = {
  next: x => console.log(`Observer got a next value: ${x}`),
  error: err => console.log(`Observer got an error: ${err}`),
  complete: () => console.log('Observer got a complete notification')
};

// Execute with the observer object
myObservable.subscribe(myObserver);

// Logs:
// Observer got a next value: 1
// Observer got a next value: 2
// Observer got a next value: 3
// Observer got a complete notification
```

Alternatively, the `subscribe()` method can accept callback `function` definitions in line, for `next`, `error`, and `complete` handlers.  For example, the following `subscribe()` call is the same as the one that specifies the predefined observer:

```ts
const myObserver = {
  next: x => console.log(`Observer got a next value: ${x}`),
  error: err => console.log(`Observer got an error: ${err}`),
  complete: () => console.log('Observer got a complete notification')
};
```

In either case, a `next` handler is **required**; the `error` and `complete` handlers are optional.

  > **NOTE**: A `next()` function could receive, for instance, message `strings`, or event `objects`, numeric values, or structures, depending on context. As a general term, we refer to data published by an `observable` as a stream. Any type of value can be represented with an `observable`, and the values are published as a stream.

---

[Angular Docs](https://angular.io/guide/observables#subscribing)