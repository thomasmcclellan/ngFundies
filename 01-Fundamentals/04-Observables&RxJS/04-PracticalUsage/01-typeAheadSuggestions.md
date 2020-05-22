##### 5/21/2020
# Practical Usage - Type-Ahead Suggestions
`Observables` can simplify the implementation of type-ahead suggestions.  Typically, a type-ahead has to do a series of separate tasks:
  * Listen for data from an input
  * Trim the value (remove whitespace) and make sure it's a minimum length
  * Debound (so as not to send off API requests for each keystroke, but instead wait for a break in keystrokes)
  * Don't send a request if the value stays the same (i.e. rapidly hit a character, then backspace)
  * Cancel ongoing `AJAX` requests if their results will be invalidated by the updated results

Writing this in full `JS` can be quite involved.  With `observables`, you can use a simple series of `RxJS` operators:

```ts
import { fromEvent } from 'rxjs';
import { ajax } from 'rxjs/ajax';
import { debounceTime, distinctUntilChanged, filter, map, switchMap } from 'rxjs/operators';

const searchBox = document.getElementById('search-box'),
      typeAhead = fromEvent(searchBox, 'input')
        .pipe(
          map((e: KeyboardEvent) => (e.target as HTMLInputElement).value),
          filter(text => text.length > 2),
          debounceTime(10),
          distinctUntilChanged(),
          switchMap(() => ajax('/api/endpoint'))
      );

typeAhead.subscribe(data => /* Handle the data from the API */ );
```

---

[Angular Docs](https://angular.io/guide/practical-observable-usage#type-ahead-suggestions)