##### 5/13/2020
# The `RxJS` Library - `Observable` Creation `Functions`
`RxJS` offers a number of `functions` that can be used to create new `observables`. These `functions` can simplify the process of creating `observables` from things such as events, timers, promises, and so on.  For example:

```ts
import { from } from 'rxjs';

// Create an Observable out of a promise
const data = from(fetch('/api/endpoint'));
// Subscribe to begin listening for async result
data.subscribe({
  next(response) { console.log(response); },
  error(err) { console.log(`Error: ${err}`); },
  complete() { console.log('Completed'); }
});
```

```ts
import { interval } from 'rxjs';

// Create an Observable that will publish a value on an interval
const secondsCounter = interval(1000);
// Subscribe to begin publishing values
secondsCounter.subscribe(n => console.log(`It's been ${n} seconds since subscribing`));
```

```ts
import { fromEvent } from 'rxjs';

const el = document.getElementById('my-element');
// Create an Observable that will publish mouse movements
const mouseMoves = fromEvent(el, 'mousemove');
// Subscribe to start listening for mouse-move events
const subscription = mouseMoves.subscribe((evt: MouseEvent) => {
  // Log coords of mouse movements
  console.log(`Coords: ${evt.clientX} X ${evt.clientY}`);

  // When the mouse is over the upper-left of the screen, unsubscribe to stop listening for mouse movements
  if (evt.clientX < 40 && evt.clientY < 40) subscription.unsubscribe();
});
```

```ts
import { ajax } from 'rxjs/ajax';

// Create an Observable that will create an AJAX request
const apiData = ajax('/api/data');
// Subscribe to create the request 
apiData.subscribe(res => console.log(res.status, res.response));
```

---

[Angular Docs](https://angular.io/guide/rx-library#observable-creation-functions)