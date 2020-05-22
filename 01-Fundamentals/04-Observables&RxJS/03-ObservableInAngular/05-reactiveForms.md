##### 5/20/2020
# `Observables` in `Angular` - Reactive Forms
Reactive forms have properties that use `observables` to monitor form control values.  The `FormControl` properties `valueChanges` and `statusChange` contain `observables` that raise change events.  Subscribing to an `observable` form-control property is a way of triggering application logic within the component `class`.  For example:

```ts
import { OnInit } from '@angular/core';
import { FormGroup } from '@angular/forms';

@Component({
  selector: 'my-component',
  template: 'MyComponent Template'
})
export class MyComponent implements OnInit {
  nameChangeLog: string[] = [];
  hereForm: FormGroup;

  ngOnInit() {
    this.logNameChange();
  }

  logNameChange() {
    const nameControl = this.heroForm.get('name');
    nameControl.valueChanges.forEach((value: string) => this.nameChangeLog.push(value));
  }
}
```

---

[Angular Docs](https://angular.io/guide/observables-in-angular#reactive-forms)