##### 3/20/2020
# Reactive Forms - Generating Form Controls With `FormBuilder`
Creating form control instances manually can become repetitive when dealing with multiple forms.  The `FormBuilder` service provider convenient methods for generating controls.

The following section refactors the `ProfileEditor` component to use the form builder service to create form control and form group instances.

## Step 1: Importing The `FormBuilder` Class:
Import the `FormBuilder` class from the `@angular/forms` package.

```ts
import { FormBuilder } from '@angular/forms';
```

## Step 2: Injecting The `FormBuilder` Service:
The `FormBuilder` service is an injectable provider that is provided with the reactive forms module. Inject this dependency by adding it to the component constructor.

```ts
constructor(private fb: FormBuilder) { }
```

## Step 3: Generating Form Controls:
The `FormBuilder` service has three methods:  `control()`, `group()`, and `array()`.  These are factory methods for generating instances in your component classes including form controls, form groups, and form arrays.

Use the `group` method to create the `profileForm` controls.

```ts
import { Component } from '@angular/core';
import { FormBuilder } from '@angular/forms';

@Component({
  selector: 'app-profile-editor',
  templateUrl: './profile-editor.component.ts',
  styleUrls: ['./profile-editor.component.css']
})
export class ProfileEditorComponent {

  constructor(private fb: FormBuilder) { }

  profileForm = this.fb.group({
    firstName: [''],
    lastName: [''],
    address: this.fb.group({
      street: [''],
      city: [''],
      state: [''],
      zip: ['']
    })
  });
}
```

In this example above, you use the `group()` method with the same `object` to define the properties in the method.  The value for each control name is an `array` containing the initial value as the first item in the `array`.

  > **NOTE**: You can define the control with just the value, but if your control needs sync or async validation, add sync and async validators as the second and third items in the `array`.

Compare using the form builder to creating the instances manually.

```ts
// Instance:
profileForm = new FormBuilder({
  firstName: new FormControl(''),
  lastName: new FormControl(''),
  address: new FormGroup({
    street: new FormControl(''),
    city: new FormControl(''),
    state: new FormControl(''),
    zip: new FormControl(''),
  })
});
```

```ts
// Form Builder:
profileForm = this.fb.group({
    firstName: [''],
    lastName: [''],
    address: this.fb.group({
      street: [''],
      city: [''],
      state: [''],
      zip: ['']
    })
  });
```

---

[Angular Docs](https://angular.io/guide/reactive-forms#generating-form-controls-with-formbuilder)