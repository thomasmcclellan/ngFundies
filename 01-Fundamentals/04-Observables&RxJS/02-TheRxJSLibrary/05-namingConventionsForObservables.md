##### 5/13/2020
# The `RxJS` Library - Naming Conventions for `Observables`
Because `Angular` applications are mostly written in `TS`, you will typically know when a variable is an `observable`.  Although the `Angular` framework does not enforce a naming convention for `observables`, you will often see `observables` named with a training `$` sign.

This can be useful when scanning through code and looking for `observable` values.  Also, if you want a property to store the most recent value from an `observable`, it can be convenient to simply use the same name with or without the `$`.

For example:

```ts
import { Component } from '@angular/core';
import { Observable } from 'rxjs';

@Component({
  selector: 'app-stopwatch',
  templateUrl: './stopwatch.component.html'
})
export class StopwatchComponent {
  stopwatchValue: number;
  stopwatchValue$: Observable<number>;

  start() : void {
    this.stopwatchValue$.subscribe(num => this.stopwatchValue = num);
  }
}
```

---

[Angular Docs](https://angular.io/guide/rx-library#naming-conventions-for-observables)