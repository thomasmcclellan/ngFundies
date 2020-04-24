##### 4/23/2020
# Form Validation - Cross Field Validation
This section shows how to perform cross field validation.  It assumes some basic knowledge of creating custom validators.

In the following section, we will make sure that our heroes do not reveal their true identities by fill out out the Hero Form. We will do that by validating that the hero names and alter egos do not match.

---

## Adding to Reactive Forms:
The form has the following structures:

```ts
const heroForm = new FormGroup({
  'name': new FormControl(),
  'alterEgo': new FormControl(),
  'power': new FormControl()
});
```

Notice that the name and alterEgo are sibling controls.  To evaluate both controls in a single custom validator, we should perform the validation in a common ancestor control:  the `FormGroup`.  That way, we an query the `FormGroup` for the child controls which will also use to compare their values.

To add a validator to the `FormGroup`, pass the new validator in as the second argument on creation.

```ts
const heroForm = new FormGroup({
  'name': new FormControl(),
  'alterEgo': new FormControl(),
  'power': new FormControl()
}, { validators: identityRevealedValidator });
```

The validator code is as follows:

```ts
// A hero's name can't match the hero's alter ego
export class identityRevealValidator: ValidatorFn = (control: FormGroup): ValidationErrors | null => {
  const name = control.get('name'),
        alterEgo = control.get('alterEgo');

  return name && alterEgo && name.value === alterEgo.value ? { 'identityRevealed': true } : null;
};
```

The identity validator implements the `ValidatorFn` interface.  It takes an `Angular` control object as an argument and returns either `null` if the form is valid, or `ValidationErrors` otherwise.

First, we retrieve the child controls by calling the `FormGroup`'s `get` method.  Then we simply compare the values of the `name` and `alterEgo` controls.

If the values do not match, the hero's identity remains secret, and we can safely return `null`.  Otherwise, the hero's identity is revealed and we must mark the form as invalid by returning an error `object`.

Next, to provide better user experience, we show an appropriate error message when the form is invalid.

```html
<div 
  *ngIf="heroForm.errors?.identityRevealed && (heroForm.touched || heroForm.dirty)"
  class="cross-validation-error-message alert alert-danger"
>
  Name cannot match alter ego.
</div>
```

Note that we check if:
  * The `FormGroup` has the cross validation error returned by the `identityRevealed` validator
  * The user is yet to interact with the form

---

## Adding to Template-Driven Forms:
First we must create a directive that will wrap the validator `function`.  We provide it as the validator using the `NG_VALIDATORS` token.  If you are not sure why, or you do not fully understand the syntax, revisit the previous section.

```ts
@Directive({
  selector: '[appIdentityRevealed]',
  providers: [{ 
    provide: NG_VALIDATORS,
    useExisting: IdentityRevealedValidatorDirective,
    multi: true
  }]
})
export class IdentityRevealedValidatorDirective implements Validators {
  validate(control: AbstractControl): ValidationErrors {
    return identityRevealedValidator(control);
  }
}
```

Next, we have to add the directive to the `HTML` template.  Since the validator must be registered at the highest level in the form, we put the directive on the `form` tag.

```html
<form #heroForm="ngForm" appIdentityRevealed>
```

To provide better user experience, we show an appropriate error message when the form is invalid.

```html
<div 
  *ngIf="heroForm.errors?.identityRevealed && (heroForm.touched || heroForm.dirty) "
  class="cross-validation-error-message alert alert-danger"
>
  Name cannot match alter ego.
</div>
```

Note that we check if:
  * The form has the cross validation error returned by the `identityRevealed` validator
  * The user is yet to interact with the form

This completes the cross validation example.  We managed to:
  * Validate the form based on the values of two sibling controls
  * Show a descriptive error message after the user interacted with the form and validation failed

---

[Angular Docs](https://angular.io/guide/form-validation#control-status-css-classes)