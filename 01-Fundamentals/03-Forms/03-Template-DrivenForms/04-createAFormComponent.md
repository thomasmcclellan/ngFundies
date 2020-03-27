##### 3/27/2020
# Template-Driven Forms - Create A Form Component
An `Angular` form has two parts:  an `HTML`-based _template_ and a component _class_ to handle data and user interactions programmatically.  Begin with the `class` because it states, in brief, what the hero editor can do.

Using the `Angular` CLI command `ng g c`, generate a new component named `HeroForm`:

```
ng g c HeroForm
```

With this content:

```ts
import { Component } from '@angular/core';
import { Hero } from '../hero';

@Component({
  selector: 'app-hero-form',
  templateUrl: './hero-form.component.html',
  styleUrls: ['./hero-form.component.css']
})
export class HeroFormComponent {
  powers = [
    'Really smart',
    'Super flexible',
    'Super hot',
    'Weather changer'
  ];
  model = new Hero(18, 'Dr. IQ', this.powers[0], 'Chuck Overstreet');
  submitted = false;

  onSubmit() { this.submitted = true; }

  // TODO: Remote this when we're done
  get diagnostic() { return JSON.stringify(this.model); }
}
```

There's nothing special about this component, nothing form-specific, nothing to distinguish it from any component you've written before.

Understanding this component requires only the `Angular` concepts overed in previous pages.
  * The code imports the `Angular` core library and the `Hero` model you just created
  * The `@Component` selector value of `app-hero-form` means you can drop this form in a parent template with a `<app-hero-form></app-hero-form>` tag
  * The `templateUrl` property points to a separate file for the template `HTML`
  * YOu defined dummy data for the `model` and `powers`, as befits this demo

Down the road, you can inject a data service to get and save real data or perhaps expose these properties as inputs and outputs for binding to a parent component.  This is not a concern now and these future changes won't affect the form.
  * YOu added a `diagnostic` property to return a `JSON` representation of the model.  It'll help you see what you're doing during development; you've left yourself a cleanup note to discard it later

---

[Angular Docs](https://angular.io/guide/forms#create-the-hero-model-class)