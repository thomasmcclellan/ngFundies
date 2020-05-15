##### 5/11/2020
# Observable Overview - Creating `Observables`
Use the `Observable` constructor to create an `observable` stream of any type.  The constructor takes as its argument the subscriber `function` to run when the `observable`'s `subscribe()` method executes.  A subscriber `function` receives an `Observer` object, and can publish values to the observer's `next()` method.

For example, to create an `observable` equivalent to the `of(1, 2, 3)` above, you could do something like this:

```ts
// This function runs when subscribe() is called
function sequenceSubscriber(observer) {
  // Synchronously deliver 1, 2, and 3, then complete
  observer.next(1);
  observer.next(2);
  observer.next(3);
  observer.complete();

  // Unsubscribe function doesn't need to do anything in this because values are delivered synchronously
  return { unsubscribe() {} };
}

// Create a new Observable that will deliver the above sequence
const sequence = new Observable(sequenceSubscriber);

// Execute the Observable and print the result of each notification
sequence.subscribe({
  next(num) { console.log(num); },
  complete() { console.log('finished sequence'); }
});

// Logs:
// 1
// 2
// 3
// finished sequence
```

To take this example a little further, we can create an `observable` that publishes events.  In this example, the subscriber `function` is defined inline.

```ts
function fromEvent(target, eventName) {
  return new Observable(observer => {
    const handler = e => observer.next(e);

    // Add the event handler to the target
    target.addEventListener(eventName, handler);

    return () => {
      // Detach the event handler from the target
      target.removeEventListener(eventName, handler);
    };
  });
}
```

Now you can use this `function` to create an `observable` that publishes _keydown_ events:

```ts
const ESC_KEY = 27,
      nameInput = document.getElementById('name') as HTMLInputElement,
      subscription = fromEvent(nameInput, 'keydown')
        .subscribe((e: KeyboardEvent) => {
          if (e.keyCode === ESC_KEY) nameInput.value = '';
        });
```

---

[Angular Docs](https://angular.io/guide/observables#creating-observables)