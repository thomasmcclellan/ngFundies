##### 5/13/2020
# The `RxJS` Library - Error Handling
In addition to the `error()` handler that you provide on subscription, `RxJS` provides the `catchError` operator that lets you handle known error in the `observable` recipe.

For instance, suppose you have an `observable` that makes an API request and maps to the response from the server.  If the server returns an error or the value doesn't exist, an error is produced.  If you catch this error and supply a default value, your stream continues to process values rather than erroring out.

Here's an example of using the `catchError` operator to do this:

```ts
import { ajax } from 'rxjs/ajax';
import { map, catchError } from 'rxjs/operators';

// Return 'response' from the API. 
// If an error happens, return an empty array
const apiData = ajax('/api/data')
  .pipe(map(res => {
    if (!res.response) throw new Error('Value expected!');

    return res.response;
  }),
  catchError(err => of([]))
  );

  apiData.subscribe({
    next(x) { console.log(`data: ${x}`); },
    error(err) { console.log('errors already caught...will not run'); }
  });
```

---

## Retry Failed `Observable`:
Where the `catchError` operator provides a simple path or recovery, the `retry` operator lets you retry a failed request.

Use the `retry` operator before the `catchError` operator.  It resubscribes to the original source `observable`, which can then re-run the full sequence of actions that resulted in the error.  If this includes an HTTP request, it will retry that HTTP request.

The following converts the previous example to retry the request before catching the error:

```ts
import { ajax } from 'rxjs/ajax';
import { map, retry, catchError } from 'rxjs/operators';

const apiData = ajax('/api/data')
  .pipe(
    retry(3), // retries up to 3 times before failing
    map(res => {
      if (!res.response) throw new Error('Value expected!');

      return res.response;
    }),
    catchError(err => of([]))
  );

  apiData.subscribe({
    next(x) { console.log(`data: ${x}`); },
    error(err) { console.log('errors already caught...will not run'); }
  });
```

  > **WARNING**: Do not retry **authentication** requests, since these should only be initiated by user action.  We don't want to lock out user accounts with repeated login requests that the user has not initiated.

---

[Angular Docs](https://angular.io/guide/rx-library#error-handling)