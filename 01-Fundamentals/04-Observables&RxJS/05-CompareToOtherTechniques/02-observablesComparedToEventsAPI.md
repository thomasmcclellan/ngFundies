##### 5/27/2020
# Compare to Other Techniques - `Observables` Compared to Events API
`Observables` are very similar to event handlers that use the events API. Both techniques define notification handlers, and use them to process multiple values delivered over time. Subscribing to an `observable` is equivalent to adding an event listener. One significant difference is that you can configure an `observable` to transform an event before passing the event to the handler.

Using `observables` to handle events and asynchronous operations can have the advantage of greater consistency in contexts such as HTTP requests.

Here are some code samples that illustrate how the same kind of operation is defined using `observables` and the events API.

## Creation and Cancellation:
`Observables`:

```ts
// Setup
let clicks$ = fromEvent(buttonEl, 'click');

// Begin listening
let subscription = clicks$
  .subscribe(e => console.log('Clicked', e))

// Stop listening
subscription.unsubscribe();
```

Events API:

```ts
function handler(e) {
  console.log('Clicked', e);
}
// Setup & begin listening
button.addEventListener('click', handler);
// Stop listening
button.removeEventListener('click', handler);
```

## Subscription:
`Observables`:

```ts
observable.subscribe(() => {
  // notification handlers here
});
```

Events API:

```ts
element.addEventListener(eventName, (event) => {
  // notification handler here
});
```

## Configuration:
`Observables`:

Listen for keystrokes, but provide a stream representing the value in the input.


```ts
fromEvent(inputEl, 'keydown').pipe(
  map(e => e.target.value)
);
```

Events API:

Does not support configuration.

```ts
element.addEventListener(eventName, event => {
  // Cannot change the passed Event into another
  // value before it gets to the handler
});
```

---

[Angular Docs](https://angular.io/guide/comparing-observables#observables-compared-to-events-api)