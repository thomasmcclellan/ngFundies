##### 5/12/2020
# Observable Overview - Multicasting
A typical `observable` creates a new, independent execution for each subscribed observer.  When an observer subscribes, the `observable` wires up an event handler and delivers values to that observer.  When a second observer subscribes, the `observable` the wires up a new event handler and delivers values to that second observer in a separate execution.

Sometimes, instead of starting an independent execution for each subscriber, you want each subscription to get the same values--even if values have already started emitting.  This might be the case with something like an `observable` of clicks on the document `object`.

_Multicasting_ is the practice of broadcasting to a list of multiple subscribers in a single execution.  with a multicasting `observable`, you don't register multiple listeners on the document, but instead re-use the first listener and send values out to each subscriber.

When creating an `observable` you should determine how you want that `observable` to be used and whether or not you want to multicast its values.

Let's look at an example that counts from 1 to 3, with a one-second delay after each number emitted.

```ts
function sequenceSubscriber(observer) {
  const seq: Array<any> = [1, 2, 3];
  let timeoutId;

  // Will run through an array of numbers, emitting one value per second until it gets to the end of the array
  function doSequence(arr, idx) {
    timeoutId = setTimeout(() => {
      observer.next(arr[idx]);

      if (idx === arr.length -1) observer.complete();
      else doSequence(arr, ++idx);
    }, 1000);
  }

  doSequence(seq, 0);

  // Unsubscribe should clear the timeout to stop execution
  return { unsubscribe() {
    clearTimeout(timeoutId);
  }};
}

// Create a new Observable that will deliver the above sequence
const sequence = new Observable(sequenceSubscriber);

sequence.subscribe({
  next(num) { console.log(num); },
  complete() { console.log('Finished sequence'); }
});

// Logs:
// (at 1 second): 1
// (at 2 seconds): 2
// (at 3 seconds): 3
// (at 3 seconds): Finished sequence
```

Notice that if you subscribe twice, there will be two separate streams, each emitting values every second.  It looks something like this:

```ts
// Subscribe starts the clock, and will emit after 1 second
sequence.subscribe({
  next(num) { console.log(`1st subscribe: ${num}`); },
  complete() { console.log('1st sequence finished.'); }
});

// After 1/2 second, subscribe again.
setTimeout(() => {
  sequence.subscribe({
    next(num) { console.log(`2nd subscribe: ${num}`); },
    complete() { console.log('2nd sequence finished.'); }
  });
}, 500);

// Logs:
// (at 1 second): 1st subscribe: 1
// (at 1.5 seconds): 2nd subscribe: 1
// (at 2 seconds): 1st subscribe: 2
// (at 2.5 seconds): 2nd subscribe: 2
// (at 3 seconds): 1st subscribe: 3
// (at 3 seconds): 1st sequence finished
// (at 3.5 seconds): 2nd subscribe: 3
// (at 3.5 seconds): 2nd sequence finished
```

Changing the `observable` to be multicasting could look something like this:

```ts
function multicastSequenceSubscriber() {
  const seq = [1, 2, 3],
  // Keep track of each observer (one for every active subscription)
        observers = [];
  // Still a single timeoutId because there will only ever be one set of values being generated, multicasted to each subscriber
  let timeoutId;

  // Return the subscriber function (runs when subscribe() function is invoked)
  return (observer) => {
    observers.push(observer);
    
    // When this is the first subscription, start the sequence
    if (observers.length === 1) {
      timeoutId = doSequence({
        next(val) {
          // Iterate through observers and notify all subscriptions
          observers.forEach(obs => obs.next(val));
        },
        complete() {
          // Notify all complete callbacks
          observers.slice(0).forEach(obs => obs.complete());
        }
      }, seq, 0);
    }

    return {
      unsubscribe() {
        // Remove from the observers array so it's no longer notified
        observers.splice(observers.indexOf(observer), 1);
        // If there's no more listeners, do cleanup
        if (observers.length === 0) {
          clearTimeout(timeoutId);
        }
      }
    };
  };
}

// Run through an array of numbers, emitting one value per second until it gets to the end of the array.
function doSequence(observer, arr, idx) {
  return setTimeout(() => {
    observer.next(arr[idx]);
    
    if (idx === arr.length - 1) observer.complete();
    else doSequence(observer, arr, ++idx);
  }, 1000);
}

// Create a new Observable that will deliver the above sequence
const multicastSequence = new Observable(multicastSequenceSubscriber());

// Subscribe starts the clock, and begins to emit after 1 second
multicastSequence.subscribe({
  next(num) { console.log(`1st subscribe: ${num}`); },
  complete() { console.log('1st sequence finished.'); }
});

// After 1 1/2 seconds, subscribe again (should "miss" the first value).
setTimeout(() => {
  multicastSequence.subscribe({
    next(num) { console.log(`2nd subscribe: ${num}`); },
    complete() { console.log('2nd sequence finished.'); }
  });
}, 1500);

// Logs:
// (at 1 second): 1st subscribe: 1
// (at 2 seconds): 1st subscribe: 2
// (at 2 seconds): 2nd subscribe: 2
// (at 3 seconds): 1st subscribe: 3
// (at 3 seconds): 1st sequence finished
// (at 3 seconds): 2nd subscribe: 3
// (at 3 seconds): 2nd sequence finished
```

  > Multicasting `observables` take a bit more setup, but they can be useful for certain applications.  Later we will look at tools that simplify the process of multicasting, allowing you to take any `observable` and make it multicasting.

---

[Angular Docs](https://angular.io/guide/observables#multicasting)