##### 4/21/2020
# Form Validation - Customer Validators
Since the built-in validators won't always match the exact use case of your application, sometimes you'll want to create a customer validator.

Consider the `forbiddenNameValidator` `function` from the previous examples in this section.  Here's what the definition of that `function` looks like:

```ts
// A hero's name can't match the given regular expression
export function forbiddenNameValidator(nameRe: RegExp) : ValidatorFn {
  return (control: AbstractControl): { [key: string]: any } | null => {
    const forbidden = nameRe.test(control.value);
    return forbidden ? { 'forbiddenName': { value: control.value }} : null;
  };
}
```

The `function` is actually a factory that takes a `RegExp` to detect a _specific_ forbidden name and returns a validator `function`.

In this sample, the forbidden name is 'bob', so the validator will reject any hero name containing 'bob'.  Elsewhere it could reject 'alice' or any name that the configuring `RegExp` matches.

The `forbiddenNameValidator` factory returns the configured validator `function`.  That `function` takes an `Angular` control `object` and returns _either_ `null` if the control value is valid, _or_ a validation error `object`.  The validation error `object` typically has a property whose name is the validation key, `forbiddenName`, and whose value is an arbitrary dictionary of values that you could insert into an error message, `{name}`.

Custom async validators are similar to sync validators, but they must instead return a `Promise` or `Observable` that later emits `null` or a validation error `object`. In the case of an `Observable`, the `Observable` must complete, at which point the form uses the last value emitted for validation.

## Adding to Reactive Forms:
In reactive forms, custom validators are fairly simple to add.  All you have to do is pass the `function` directly to the `FormControl`.

```ts
this.heroForm = new FormGroup({
  'name': new FormControl(this.hero.name, [
    Validators.required,
    Validators.minLength(4),
    forbiddenNameValidator(/bob/i) // here is how you pass in the custom validator
  ]),
  'alterEgo': new FormControl(this.hero.alterEgo),
  'power': new FormControl(this.hero.power, Validators.required)
});
```

## Adding to Template-Driven Forms:
In template-driven forms, you don't have direct access to the `FormControl` instance, so you can't pass the validator in like you can for reactive forms.  Instead, you need to add a directive to the template.

The corresponding `ForbiddenValidatorDirective` serves as a wrapper around the `forbiddenNameValidator`.

`Angular` recognizes the directive's role int he validation process because the directive registers itself with the `NG_VALIDATORS` provider, a provider with an extensible collection of validators.

```ts
providers: [{ 
  provide: NG_VALIDATORS, 
  useExisting: ForbiddenValidatorDirective, 
  multi: true
}]
```

The directive `class` then implements the `Validator` interface, so that it can easily integrate with `Angular` forms.  Here is the rest of the directive to help you get an idea of how it all comes together:

```ts
@Directive({
  selector: '[appForbiddenName]',
  providers: [{ 
    provide: NG_VALIDATORS, 
    useExisting: ForbiddenValidatorDirective, 
    multi: true
  }]
})
export class ForbiddenValidatorDirective implements Validator {
  @Input('appForbiddenName') forbiddenName: string;

  validate(control: AbstractControl) : { [ key: string]: any } | null {
    return this.forbiddenName ? 
      forbiddenNameValidator(new RegExp(this.forbiddenName, 'i'))(control) : 
      null;
  }
}
```

Once the `ForbiddenValidatorDirective` is ready, you can simply add its selector, `appForbiddenName`, to any input element to activate it.  For example:

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
```

  > You may have noticed that the custom validation directive is instantiated with `useExisting` rather than `useClass`.  The registered validator must be _this instance_ of the `ForbiddenValidatorDirective`--the instance in the form with its `forbiddenName` property bound to 'bob'.  If you were to replace `useExisting` with `useClass`, then you'd be registering a new class instance, one that doesn't have a `forbiddenName`.

---

[Angular Docs](https://angular.io/guide/form-validation#custom-validators)