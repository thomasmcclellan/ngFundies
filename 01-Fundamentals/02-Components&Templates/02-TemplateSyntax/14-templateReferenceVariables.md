##### 11/01/2019
# Template Syntax - Template Reference Variables `#var`
A **template reference variable** is often a reference to a `DOM` element within a template.  It can also refer to a directive (which contains a component), an element, [TemplateRef](https://angular.io/api/core/TemplateRef), or a [web component](https://developer.mozilla.org/en-US/docs/Web/Web_Components).

Use the hash symbol (`#`) to declare a reference variable.  the following reference variable, `#phone`, declares a phone variable on an `<input>` element:

```html
<input #phone placeholder="phone number">
```

You can refer to a template reference variable anywhere in the component's template.  Here, a `<button>` further down the template refers to the phone variable.

```html
<input #phone placeholder="phone number">

<!-- ... -->

<!-- phone refers to the input element; pass its 'value' to an event handler -->
<button (click)="callPhone(phone.value)">Call</button>
```

## How a Reference Variable Gets Its Value:
In most cases, `Angular` sets the reference variable's value to the element on which it is declared.  In the previous example, `phone` refers to the phone number `<input>`.  The button's click handler passes the `<input>` value to the component's `callPhone()` method.

The `NgForm` directive can change that behavior and set the value to something else.  In the following example, the template reference variable, `itemForm`, appears three times separated by `HTML`.

```html
<form #itemForm="ngForm" (ngSubmit)="onSubmit(itemForm)">
  <label for="name">
    Name
    <input 
      class="form-control" 
      name="name" 
      ngModel 
      required
    >
  </label>
</form>

<div [hidden]="!itemForm.form.valid">
  <p>{{ submitMessage }}
</div>
```

The reference value of `itemForm`, without the `ngForm` attribute value, would be the [HTMLFormElement](https://developer.mozilla.org/en-US/docs/Web/API/HTMLFormElement).  There is, however, a difference between a Component and a Directive in that a Component will be referenced without specifying the attribute value, and a Directive will not change the implicit reference (that is, the element).

However, with `NgForm`, `itemForm` is a reference to the `NgForm` directive with the ability to track the value and validity  of every control in the form.

The native `<form>` element doesn't have a `form` property, but the `NgForm` directive does, which allows disabling the submit button if the `itemForm.form.valid` is invalid and passing the entire form control tree to the parent component's `onSubmit()` method.

## Template Reference Variable Considerations:
A template _reference_ variable (`#phone`) is not the same as a template _input_ variable (`let phone`) such as in an `*ngFor`.

The scope of a reference variable is the entire template.  So don't define the same variable name more than once in the same template as the runtime value will be unpredictable.

### Alternative Syntax:
You can use the `ref-` prefix alternatively to `#`.  This example declares the `fax` variable as `ref-fax` instead of `#fax`.

```html
<input ref-fax placehold="fax number">
<button (click)="callFax(fax.value)">Fax</button>
```

---

[Angular Docs](https://angular.io/guide/template-syntax#template-reference-variables-var)