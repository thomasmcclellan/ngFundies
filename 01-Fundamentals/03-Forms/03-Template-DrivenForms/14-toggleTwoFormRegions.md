##### 4/10/2020
# Template-Driven Forms - Toggle Two Form Regions (Extra Credit)
Submitting the form isn't terribly dramatic at the moment.

  > An unsurprising observation for a demo.  To be honest, jazzing it up won't teach you anything new about forms.  But this is an opportunity to exercise some of your newly won binding skills.  If you aren't interested, skip to this page's conclusion.

For a more strikingly visual effect, hide the data entry area and display something else.

Wrap the form in a `<div>` and bind its `hidden` property to the `HeroFormComponent.submitted` property:

```html
<div [hidden]="submitted">
  <h1>Hero Form</h1>
  <form (ngSubmit)="onSubmit()" #heroForm="ngForm">
  <!-- ...all of the form... -->
  </form>
</div>
```

The main form is visible from the start because the `submitted` property is false until you submit the form, as this fragment from the `HeroFormComponent` shows:

```ts
submitted: boolean = false;

onSubmit() : void { this.submitted = true; }
```

When you click the _Submit_ button, the `submitted` flag becomes `true` and the form disappears as planned.

Now the app needs to show something else while the form is in the submitted state.  And the following `HTML` below the `<div>` wrapper you just wrote:

```html
<div [hidden]="!submitted">
  <h2>You submitted the following:</h2>
  <div class="row">
    <div class="col-xs-3">Name</div>
    <div class="col-xs-9">{{ model.name }}</div>
  </div>
  <div class="row">
    <div class="col-xs-3">Alter Ego</div>
    <div class="col-xs-9">{{ model.alterEgo }}</div>
  </div>
  <div class="row">
    <div class="col-xs-3">Power</div>
    <div class="col-xs-9">{{ model.power }}</div>
  </div>
  <br>
  <button class="btn btn-primary" (click)="submitted=false">Edit</button>
</div>
```

Here's the hero again, displayed read-only with interpolation bindings.  This `<div>` appears only while the component is in the submitted state.

The `HTML` includes an _Edit_ button whose click event is bound to an expression that clears the `submitted` flag.

When you click the _Edit_ button, this block disappears and the editable form reappears.

---

[Angular Docs](https://angular.io/guide/forms#toggle-two-form-regions-extra-credit)