##### 5/26/2020
# Compare to Other Techniques - `Observables` Compared to `Promises`
`Observables` are often compared to `promises`.  Here are some key differences:

| `Observables` | `Promises` | Outcome |
|---|---|---|
| `Observables` are declarative; computation does not start until subscription. | `Promises` execute immediately on creation. | This makes `observables` useful for defining recipes that can be run whenever you need the result. | 
| `Observables` provide many values. | `Promises` provide one. | This makes `observables` useful for getting multiple values over time. |
| `Observables` differentiate between chaining and subscription. | `Promises` only have `.then()` clauses. | This makes `observables` useful for creating complex transformation recipes to be used by other parts of the system, without causing the work to be executed. |
| `Observables` `subscribe()` is responsible for handling errors. | `Promises` push errors to the child `promises`. | This makes `observables` useful for centralized and predictable error handling. |

---

## Creation and Subscription:
`Observables` are not executed until the consumer subscribes.  The `subscribe()` executes the defined behavior once, and it can be called again.  Each subscription has its own computation. Resubscription causes recomputation of values.

```ts
// Declare a publishing operation
const observable = new Observable<number>(observer => {
  // Subscriber fn...
});

// Initiate execution
observable.subscribe(() => {
  // Observer handles notifications
});
```

`Promises` execute immediately, and just once.  The computation of the result is initiated when the `promise` is created.  There is no way to restart work.  All `then` clauses (subscriptions) share the same computation.

```ts
// Initiate execution
const promise = new Promise<number>((resolve, reject) => {
  // Execute fn...
});

promise.then(value => {
  // Handle result here
});
```

---

## Chaining: 
`Observables` differentiate between transformation `function` such as a map and subscription.  Only subscription activates the subscriber `function` to start computing the values.

```ts
observable.pipe(map(v => 2 * v));
```

`Promises` do not differentiate between the last `.then()` clauses (equivalent to subscription) and intermediate `.then()` clauses (equivalent to map).

```ts
promise.then(v => 2 * v);
```

---

## Cancellation: 
`Observable` subscriptions are cancellable.  Unsubscribing removes the listener from receiving further values, and notifies the subscriber `function` to cancel work.

```ts
const subscription = observable.subscribe(() => {
  // Observer handles notifications
});

subscription.unsubscribe();
```

`Promises` are not cancellable.

---

## Error Handling:
`Observable` execution errors are delivered to the subscriber's error handler, and the subscriber automatically unsubscribes from the `observable`.

```ts
observable.subscribe(() => {
  throw Error('my error');
});
```

`Promises` push errors to the child `promises`.

```ts
promise.then(() => {
  throw Error('my error');
});
```

---

[Angular Docs](https://angular.io/guide/comparing-observables#observables-compared-to-promises)