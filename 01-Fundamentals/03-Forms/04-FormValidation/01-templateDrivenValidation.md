##### 4/17/2020
# Form Validation - Template-Driven Validation
To add validation to a template-driven form, you add the same validation attributes as you would with [native `HTML` form validation](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/HTML5/Constraint_validation).  `Angular` uses directives to match these attributes with validator `functions` in the framework.

Every time the value of a form control changes, `Angular` runs validation and generates either a list of validation errors, which results in an INVALID status, or `null`, which results in a VALID status.

You can then inspect the control's state by exporting `ngModel` to a local template variable.  The following example exports `NgModel` into a variable called `name`:

```html
<input
  id="name"
  name="name"
  class="form-control"
  required
  minlength="4"
  appForbiddenName="bob"
  [(ngModel)]="hero.name"
  #name="ngModel"
>
<div
  *ngIf="name.invalid && (name.dirty || name.touched)"
  class = "alert alert-danger"
>
  <div *ngIf="name.errors.required">
    Name is required.
  </div>
  <div *ngIf="name.errors.minlength">
    Name must be at least 4 characters long.
  </div>
  <div *ngIf="name.errors.forbiddenName">
    Name name cannot be Bob.
  </div>
</div>
```

Note the following:
  * The `<input>` element carries the `HTML` validation attributes: `required` and `minlength`.  It also carries a custom validator directive, `forbiddenName`.
  * `#name="ngModel"` exports `NgModel` into a local variable called `name`.  `NgModel` mirrors many of the properties of its underlying `FormControl` instance, so you can use this in the template to check for control states such as `valid` and `dirty`.
  * The `*ngIf` on the `<div>` element reveals a set of nested message `div`s but only if the `name` is invalid and the control is either `dirty` or `touched`.
  * Each nested `<div>` can present a custom message for one fo the possible validation errors.  There are messages for `required`, `minlength`, and `forbiddenName`.

  > **Why check _dirty_ and _touched_?**
  >
  > You may not want you application to display errors before the user has a change to edit the form.  The checks for `dirty` and `touched` prevent errors for showing until the user does one of the two things:
  >   1. Changes the value, turning the control `dirty`
  >   2. Blurs the form control element, setting the control to touched

---

[Angular Docs](https://angular.io/guide/form-validation#template-driven-validation)