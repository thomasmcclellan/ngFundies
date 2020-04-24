##### 4/03/2020
# Template-Driven Forms - Two-Way Binding With `ngModel`
Running the app right now would be disappointing.

![Hero Form](../../../Assets/heroForm3.png)

You don't see her data because you're not binding the the `Hero` yet.  You know how to do that from earlier pages.  Displaying Data teaches property binding.  User Input shows how to listen for `DOM` events with an event binding and how to update a component proper with the displayed value.

Now you need to display, listen, and extract at the same time.

You could use the techniques you already know, but instead you'll use the new `[(ngModel)]` syntax, which makes binding the form to the model easy.

Find the `<input>` tag for _Name_ and update it like this:

```html
<input
  type="text"
  class="form-control"
  id="name"
  required
  [(ngModel)]="model.name"
  name="name"
>
<!-- TODO: Remove this: {{ model.name }} -->
```

  > You added a diagnostic interpolation after the input tag you can see what you're doing.  You left yourself a not to throw it away when you're done.

Focus on the binding syntax: `[(ngModel)]="..."`.

You need one more addition to display the data.  Declare a template variable for the form. Update the `<form>` tag with `#heroForm="ngForm"` as follows:

```html
<form #heroForm="ngForm">
```

the variable `heroForm` is now a reference to the `NgForm` directive that governs the form as a whole.

---

## The `NgForm` Directive:
  > What `NgForm` directive?  You didn't add an [`NgForm`](https://angular.io/api/forms/NgForm) directive.
  > `Angular` did, however.  `Angular` automatically creates and attaches an `NgForm` directive to the `<form>` tag.
  > The `NgForm` directives supplements the `form` element with additional features.  It holds the controls you created for the elements with an `ngModel` directive and `name` attribute, and monitors their properties, including their validity.  It also has its own `valid` property which is `true` only _if every contained control_ is valid.

If you ran the app now and started typing in the _Name_ input box, adding and deleting characters, you'd see them appear and disappear from the interpolated text.  At some point it might look like this:

![`ngModel` In Action](../../../Assets/ngModel.png)

The diagnostic is evidence that values really are flowing from the input box to the model and back again.

  > That's _two-way data binding_!

Notice that you also added a `name` attribute to the `<input>` tag and set it to 'name', which makes sense for the hero's name.  Any unique value will do, but using a descriptive name is helpful.  Defining a `name` attribute is a requirement when using `[(ngModel)]` in combination with a form.

  > Internally, `Angular` creates `FormControl` instances and registers them with an `NgForm` directive that `angular` attached to the `<form>` tag.  Each `FormControl` is registered under the name you assigned to the `name` attribute.

Add similar `[(ngModel)]` bindings and `name` attributes to _Alter Ego_ and _Hero Power_.  You'll ditch the input box binding message and add a new binding (at the top) to the component's `diagnostic` property.  Then you can confirm that two-way data binding works _for the entire hero model_.

After revision, the core of the form should look like this:

```html
{{diagnostic}}
<div class="form-group">
  <label for="name">Name</label>
  <input 
    type="text" 
    class="form-control" 
    id="name"
    required
    [(ngModel)]="model.name" 
    name="name"
  >
</div>

<div class="form-group">
  <label for="alterEgo">Alter Ego</label>
  <input 
    type="text"  
    class="form-control" 
    id="alterEgo"
    [(ngModel)]="model.alterEgo" 
    name="alterEgo"
  >
</div>

<div class="form-group">
  <label for="power">Hero Power</label>
  <select 
    class="form-control"  
    id="power"
    required
    [(ngModel)]="model.power" 
    name="power"
  >
    <option *ngFor="let pow of powers" [value]="pow">{{ pow }}</option>
  </select>
</div>
```

  * Each input element has an `id` property that is used by the `label` element's `for` attribute to match the label to its input control.
  * Each input element has a `name` property that is required by `Angular` forms to register the control with the form.

If you run tha app now and change every hero model property, the form might display like this:

![`ngModel` In Action](../../../Assets/ngModel2.png)

The diagnostic near the top of the form confirms that all of your changes are reflected in the model.

_Delete_ the `{{ diagnostic }}` binding at the top as it has served its purpose.

---

[Angular Docs](https://angular.io/guide/forms#two-way-data-binding-with-ngmodel)