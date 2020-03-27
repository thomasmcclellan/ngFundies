##### 3/20/2020
# Reactive Forms - Simple Form Validation
_Form validation_ is used to validate user input to ensure it's complete and correct.  This section covers adding a single validator to form a control and displaying the overall form status.  Form validation is covered more extensively in the [Form Validation](https://angular.io/guide/form-validation) guide.

## Step 1: Importing a Validator `Function`:
Reactive forms include a set of validator `functions` for common use cases.  These `functions` receive a control to validate against and return an error `object` or a `null` value based on the validation check.

Import the `Validators` class from the `@angular/forms` package.

```ts
import { Validators } from '@angular/forms';
```

## Step 2: Making a Field Required:
The most common validation is making a field required.  This section describes how to add a required validation to the `firstName` control.

In the `ProfileEditor` component, add the `Validators.required` static method as the second item in the `array` for the `firstName` control.

```ts
profileForm = this.fb.group({
  firstName: ['', Validators.required], // addition here
  lastName: [''],
  address: this.fb.group({
    street: [''],
    city: [''],
    state: [''],
    zip: ['']
  })
});
```

`HTML5` has a set of built-in attributes that you can use for native validation, including `required`, `minlength`, and `maxlength`.  You can take advantage of these optional attributes on your form input elements.  Add the `required` attribute to the `firstName` input element.

```html
<input 
  type="text"
  formControlName="firstName"
  required
>
```

  > **CAUTION**: Use these `HTML5` validation attributes _in combination with_ the built-in validators provided by `Angular`'s reactive forms.  Using these in combination prevents errors when the expression is changed after the template has been checked.

## Displaying Form Status:
When you add a required field to the form control, its initial status is invalid.  This invalid status propagates to the parent form group element, making its status invalid.  Access the current status of the form group instance through its `status` property.

Display the current status of `profileForm` using interpolation.

```html
<p>Form Status: {{ profileForm.status }}</p>
```

![Profile Editor](../../../Assets/profileEditor3.png)

the **Submit** button is disabled because `profileForm` is invalid due to the required `firstName` form control.  After you fill out the `firstName` input, the form becomes valid and the **Submit** button is enabled.

---

[Angular Docs](https://angular.io/guide/reactive-forms#simple-form-validation)