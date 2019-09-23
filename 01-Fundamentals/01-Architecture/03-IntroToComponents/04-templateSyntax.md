##### 9/17/2019
# Introduction to Components - Templates Syntax
A template looks like regular `HTML`, except that it also contains `Angular` **template syntax**, which alters the `HTML` based on your app's logic and the state of app and DOM data.  Your template can use _data binding_ to coordinate the app and DOM data, _pipes_ to transform data before it is displayed, and _directives_ to apply app logic to what gets displayed.

`src/app/hero.list.component.html`:
```html
<h2>Hero List</h2>

<p><i>Pick a hero from the list</i></p>
<ul>
  <li *ngFor="let hero of heroes" (click)="selectedHero(hero)">
    {{ hero.name }} 
  </li>
</ul>

<app-hero-detail *ngFor="selectedHero" [hero]="selectedHero"></app-hero-detail>
```

This template uses typical `HTML` elements like `<h2>` and `<p>`, and also includes `Angular` template-syntax elements like: `*ngFor`, `{{ hero.name }}`, `[hero]`, and `<app-hero-detail>`.  The template-syntax elements tell `Angular` how to render the `HTML` to the screen, using program logic and data.

  * The `*ngFor` directive tells `Angular` to iterate over a list
  * `{{ hero.name }}`, `(click)`, and `[hero]` bind program data to and from the DOM, responding to user input
  * The `<app-hero-detail>` tag in the example is an element that represents a new component, `HeroDetailComponent`.  It (code not shown) defines the `hero-detail` child view of `HeroListComponent`.  Notice how custom components like this mix seamlessly with native `HTML` in the same layouts.

## Data Binding:
Without a framework, you would be responsible for pushing data values into the `HTML` controls and turning user responses into actions and value updates.  Writing such push and pull logic by hand is tedious, error-prone, and a nightmare to read, as any experienced front-end `JS` programmer can attest.

`Angular` supports _two-way binding_, a mechanism for coordinating the parts of a template with the parts of a component.  Add binding markup to the template `HTML` to tell `Angular` how to connect both sides.

`src/app/hero-list.component.html` (binding):
```html
<li> {{ hero.name }}</li>
<app-hero-detail [hero]="selectedHero"></app-hero-detail>
<li (click)="selectedHero(hero)"></li>
```

  * The `{{ hero.name }}` **interpolation** displays the component's `hero.name` property value within the `<li>` element
  * The `[hero]` **property binding** passes the value of `selectedHero` from the parent `HeroListComponent` to the hero property of the child `HeroDetailComponent`
  * The `(click)` **event binding** calls the component's `selectedHero` method when the user clicks a hero's name

**Two-way data binding** (used mainly in _template-driven forms_) combines property and event binding in a single notion.

`src/app/hero-detail.component.html` (ngModel):
```html
<input [(ngModel)]="hero.name">
```

In two-way binding, a data property value flows to the input box from the component as with property binding.  The user's changes also flow back to the component, resetting the property to the latest value, as with event binding.

  > `Angular` processes _all_ data bindings once for each `JS` event cycle, from the root of the application component tree through all child components.

  > Data binding plays an important role in communication between a template and its component, adn is also important for communication between parent and child components.

## Pipes:
`Angular` pipes let you declare display-value transformations in your template `HTML`.  A class with the `@Pipe` decorator defines a function that transforms input values to output values for display in a view.

  > `Angular` defines various pipes, such as the **date pipe** and **currency pipe**; for a complete list, see the [Pipes API list](https://angular.io/api?type=pipe).  You can also define new pipes.

To specify a value transformation in an `HTML` template, use the _pipe operator_ (`|`): `{{ interpolated_value | pipe_name }}`.

You can chain pipes, sending the output of one pipe function to be transformed by another pipe function.  A pipe can also take arguments that control how it performs its transformation:

```html
<!-- Default format: output 'Sep 17, 2019' -->
<p> Today is {{ today | date }}</p>

<!-- fullDate format: output 'Tuesday, September 17, 2019' -->
<p> The date is {{ today | date:'fullDate' }}</p>

<!-- shortTime format: output '9:00 AM' -->
<p> The time is {{ today | date:'shortTime' }}</p>
```

## Directives:
`Angular` templates are _dynamic_.  When `Angular` renders them, it transforms the DOM accordingly to the instructions given by **directives**.  A directive is a class with a `@Directive()` decorator.

  > A component is technically a directive.  However, components are so distinctive and central to `Angular` applications that `Angular` defines the `@Component` decorator, which extends the `@Directive()` decorator with template-oriented features.

  > In addition to components, there are two other kinds of directives: _structural_ and _attribute_. `Angular` defines a number of directives of both kinds, and you can define your own using the `@Directive` decorator/

Just as for components, the metadata for a directive associates the decorated class with a `selector` element that you use to insert it into `HTML`.  In templates, directives typically appear within an element tag as attributes, either by name or as the target of an assignment or a binding.

---

### Structural Directives:
**Structural directives** alter the layout by adding, removing, and replacing elements in the DOM.  The example template uses two built-in structural directives to add application logic to how the view is rendered:

`src/app/hero-list.component.html` (structural):
```html
<li *ngFor="let hero of heroes"></li>
<app-hero-detail *ngIf="selectedHero"></app-hero-detail>
```

  * `*ngFor` is an _iterative_; it tells `Angular` to stamp out one `<li>` per hero in the `heroes` list
  * `*ngIf` is a _conditional_; it includes the `HeroDetail` component only if a selected hero exists

---

### Attribute Directives:
**Attribute directives** alter the appearance or behavior of an existing element.  In templates they look like regular `HTML` attributes, hence their name.

The `ngModel` directive, which implements two-way data binding, is an example of an attribute directive.  `ngModel` modifies the behavior of an existing element (typically `<input>`) by setting its display value property and responding to changed events.

`src/app/hero-detail.component.html` (ngModel):
```html
<input [(ngModel)]="hero.name">
```

  > `Angular` has more pre-defined directives that either alter the layout structure (i.e. `ngSwitch`) or modify aspects of DOM elements and components (i.e. `ngStyle` and `ngClass`).

---

[Angular Docs](https://angular.io/guide/architecture-components)