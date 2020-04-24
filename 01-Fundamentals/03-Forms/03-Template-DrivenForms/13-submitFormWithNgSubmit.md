##### 4/09/2020
# Template-Driven Forms - Submit the Form with `ngSubmit`
The user should be able to submit this form after filling it in.  The _Submit_ button at the bottom of the form does nothing on its own, but it will trigger a form submit because of its type (`type="submit"`).

The 'form submit' is useless at the moment.  To make it useful, bind the form's `ngSubmit` event property to the hero form component's `onSubmit()` method:

```html
<form (ngSubmit)="onSubmit()" #heroForm="ngForm">
```

You'd already define a template reference variable, `#heroForm`, and initialize it with the value `ngForm`.  Now, use that variable to access the form with the _Submit_ button.

You'll bind the form's overall validity via the `formForm` variable to the button's `disabled` property using an event binding.  Here's the code:

```html
<button
  type="submit"
  class="btn btn-default"
  [disabled]="!heroForm.form.valid"
>
  Submit
</button>
```

If you run the application now, you  find that the button is enabled--although it doesn't useful yet.

Now if you delete the Name, you violate the 'required' rule, which is duly noted in the error message.  The _Submit_ button is also disabled.

  > Not impressed?  Think about it for a moment.  What would you have to do to wire the button's enable/disabled state to the form's validity without `Angular`'s help?

For you, it was as simple as this:
  1. Define a template reference variable on the (enhanced) form element
  2. Refer to that variable in a button many lines away

---

[Angular Docs](https://angular.io/guide/forms#submit-the-form-with-ngsubmit)