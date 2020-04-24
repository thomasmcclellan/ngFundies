##### 4/01/2020
# Template-Driven Forms - Create An Initial `HTML` Form Template
Update the template file with the following contents:

```html
<div class="container">
  <h1>Hero Form</h1>
  <form>
    <div class="form-group">
      <label for="name">Name</label>
      <input 
        type="text"
        class="form-control"
        id="name"
        required
      >
    </div>

    <div class="form-group">
      <label for="alter-ego">Alter Ego</label>
      <input
        type="text"
        class="form-control"
        id="alter-ego"
      >
    </div>

    <button type="submit" class="btn btn-success">Submit</button>
  </form>
</div>
```

The language is simply `HTML5`.  You're presenting two of the `Hero` fields, `name` and `alterEgo`, and opening them up for user input in input boxes.

The _Name_ `<input>` control has the `HTML5` `required` attribute; the _Alter Ego_ `<input>` control does not because `alterEgo` is optional.

You added a _Submit_ button at the bottom with some classes on it for styling.

_You're not using `Angular` yet_.  There is no bindings or extra directives, just layout.

  > In template-driven forms, if you've imported `FormsModule`, you don't have to do anything to the `<form>` tag in order to make use of `FormsModule`.  Continue on to see how this works.

The `container`, `form-group`, `form-control`, and `btn` classes from **Bootstrap**.  These classes are purely cosmetic.

  > `Angular` Forms don't require a style library
  > 
  > `Angular` makes no use of the `container`, `form-group`, `form-control`, and `btn` classes or the styles of any external library.  `Angular` apps can use any `CSS` library or none at all.

To add the stylesheet, open `styles.css` and add the following import line at the top:

```css
@import url('https://unpkg.com/bootstrap@3.3.7/dist/css/bootstrap.min.css');
```

---

[Angular Docs](https://angular.io/guide/forms#create-an-initial-html-form-template)