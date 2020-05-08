##### 5/06/2020
# Observable Overview - Basic Usage and Terms
As a publisher, you create an `Observable` instance that defines a _subscriber_ `function`.  this is the `function` that is executed when a consumer calls the `subscribe()` method.  The subscriber `function` defines how to obtain or generate values or messages to be published.

To execute the `observable` you have created and begin receiving notifications, you call its `subscribe()` method, passing an _observer_.  This is a `JS` `object` that defines the handlers for the notifications you receive.  The `subscribe()` call returns a `Subscription` `object` that has an `unsubscribe()` method, which you call to stop receiving notifications.

Here's an example that demonstrates the basic usage model by showing how an `observable` could be used to provide geolocation updates.

```ts
// Create an Observable that will start listening to geolation updates when a consumer subscribes
const locations = new Observable(observer => {
  let watchId: number;

  // Simple geolocation API check provides values to publish
  if ('geolocation' in navigator) {
    watchId = navigator.geolocation.watchPosition((position: Position) => {
      observer.next(position);
    }, (error: PositionError) => {
      observer.error(error);
    });
  } else {
    observer.error('Geolocation not available');
  }

  // When the consumer unsubscribes, clean up data ready for next subscription.
  return {
    unsubscribe() {
      navigator.geolocation.clearWatch(watchId);
    }
  };
});

// Call subscribe() to start listening for updates.
const locationsSubscription = locations.subscribe({
  next(position) {
    console.log('Current Position: ', position);
  },
  error(msg) {
    console.log('Error Getting Location: ', msg);
  }
});

// Stop listening for location after 10 seconds
setTimeout(() => {
  locationsSubscription.unsubscribe();
}, 10000);
```

---

[Angular Docs](https://angular.io/guide/observables#basic-usage-and-terms)