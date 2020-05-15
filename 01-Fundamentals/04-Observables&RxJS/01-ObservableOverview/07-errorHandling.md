##### 5/13/2020
# Observable Overview - Error Handling
Because `observables` produce values asynchronously, `try/catch` will not effectively catch errors.  Instead, you handle errors by specifying an `error` callback on the observer.  Producing an error also causes the `observable` to clean up subscriptions and stop producing values.  An `observable` can either produce values (calling the `next` callback), or it can complete, calling either the `complete` or `error` callback.

```ts
myObservable.subscribe({
  next(num) { console.log(`Next num: ${num}`); },
  error(err) { console.log(`Received error: ${err}`); }
});
```

  > Error handling (and specifically recovering from an error) is coved in more detail in a later section.

---

[Angular Docs](https://angular.io/guide/observables#error-handling)