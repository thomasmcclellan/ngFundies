##### 4/20/2020
# Form Validation - Template-Driven Validation
In a reactive form, the source of truth is the component `class`.  Instead of adding validators through attributes in the template, you add validator `functions` directly to the form control model in the component `class`.   `Angular` then calls these `functions` whenever the value of the control changes.

## Validator `Functions`:
There are two types of validator `functions`: sync validators and async validators.
  * **Sync validators**: `functions` that take a control instance and immediately return either a set of validation errors or `null`.  You can pass these in as the second argument when you instantiate a `FormControl`.
  * **Async validators**: `functions` that take a control instance and return a `Promise` or `Observable` that later emits a set of validation errors or `null`.  You can pass these in as the third argument when you instantiate a `FormControl`.

  > **NOTE**: For performance reasons, `Angular` only runs async validators if all sync validators pass.  Each must complete before errors are set.

## Built-In Validators:
You can choose to write your own validator `functions`, or you can use of `Angular`'s built-in validators.

The same built-in validators that are available as attributes in template-driven forms, such as `required` and `minlength`, are all available to use as `functions` from the `Validators` class.  For a full list of built-in validators, see the [Validators](https://angular.io/api/forms/Validators) API reference.

To update the hero form to be a reactive form, you can use some of the same built-in validators--this time, in `function` form.  See below:

```ts
gnOnInit() : void {
  this.heroForm = new FormGroup({
    'name': new FormControl(this.hero.name, [
      Validators.required,
      Validators.minLength(4),
      forbiddenNameValidator(/bob/i) // Here is how you pass in the custom validator
    ]),
    'alterEgo': new FormControl(this.hero.alterEgo),
    'power': new FormControl(this.hero.power, Validators.required)
  });
}

get name() { return this.heroForm.get('name'); }
get power() { return this.heroForm.get('power'); }
```

Note that:
  * The name control sets up two built-in validators--`Validators.required` and `Validators.minLength(4)`--and one custom validator, `forbiddenNameValidator`.
  * As these validators are all sync validators, you pass them in as the second argument.
  * Support multiple validators by passing the `functions` in as an `array`.
  * This example adds a few getter methods.  In a reactive form, you can always access any form control through the `get` method on its parent group, but sometimes it's useful to define getters as shorthands for the template.

If you look at the template for the name input again, it is fairly similar to the template-driven example:

```html
<input 
  id="name" 
  class="form-control"
  formControlName="name" 
  required 
>

<div 
  *ngIf="name.invalid && (name.dirty || name.touched)"
  class="alert alert-danger"
>
  <div *ngIf="name.errors.required">
    Name is required.
  </div>
  <div *ngIf="name.errors.minlength">
    Name must be at least 4 characters long.
  </div>
  <div *ngIf="name.errors.forbiddenName">
    Name cannot be Bob.
  </div>
</div>
```

Key takeaways:
  * The form no longer exports any directives, and instead uses the `name` getter defined in the component `class`.
  * The `required` attribute is still present.  While it's not necessary for validation purposes, you may want to keep it in your template for `CSS` styling or accessibility reasons.

---

[Angular Docs](https://angular.io/guide/form-validation#reactive-form-validation)