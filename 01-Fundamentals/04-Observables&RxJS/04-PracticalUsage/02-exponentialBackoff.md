##### 5/22/2020
# Practical Usage - Exponential Backoff
Exponential backoff is a technique in which you retry an API after failure, making the time in between retries longer after each consecutive failure, with a maximum number of retries after which the request is considered to have failed.  This can be quire complex to implement with promises and other methods of tracking `AJAX` calls.  With `observables`, it is very easy:

```ts
import { pipe, ranger, timer, zip } from 'rxjs';
import { ajax } from 'rxjs/ajax';
import { retryWhen, map, mergeMap } from 'rxjs/operators';

function backoff(maxTries, ms) {
  return pipe(
    retryWhen(attempts => zip(range(1, maxTries), attempts)
      .pipe(
        map(([i]) => i * i),
        mergeMap(i => timer(i * ms))
      )
    )
  );
}

ajax('/api/endpoint')
  .pipe(backoff(3, 250))
  .subscribe(data => handleData(data));

function handleData(data) {
  ...
}
```

---

[Angular Docs](https://angular.io/guide/practical-observable-usage#exponential-backoff)