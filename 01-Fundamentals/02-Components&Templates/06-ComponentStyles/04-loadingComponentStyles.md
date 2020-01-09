##### 1/06/2020
# Component Styles - Loading Component Styles
There are several ways to add styles to a component:
  * By setting `styles` or `styleUrls` metadata
  * Inline in the template `HTML`
  * With `CSS` imports

The scoping rules outlined earlier apply to each of these loading patterns.

## Styles in Component Metadata:
You can add a `styles` `array` property to the `@Component()` decorator.

Each `string` in the `array` defines some `CSS` for this component.

```ts
@Component({
  selector: 'app-root',
  template: `
    <h1>Tour of Heroes</h1>
    <app-hero-main [hero]="hero"></app-hero-main>
  `,
  styles: ['h1 { font-weight: normal; }']
})
export class HeroAppComponent { }
```

  > **NOTE**: These styles apply _only to this component_.  they are _not inherited_ by any components nested within the template nor by any content projected into the component.

The `Angular` CLI command `ng generate component` (or `ng g c`) defines an empty `styles` `array` when you create the component with the `--inline-style` flag.

```
ng generate component hero-app --inline-style
```

## Style Files in Component Metadata:
You can load styles from external `CSS` files by adding a `styleUrls` property to the component's `@Component()` decorator:

```ts
@Component({
  selector: 'app-root',
  template: `
    <h1>Tour of Heroes</h1>
    <app-hero-main [hero]="hero"></app-hero-main>
  `,
  styleUrls: ['./hero-app.component.css']
})
export class HeroAppComponent { }
```

```css
h1 {
  font-weight: normal;
}
```

  > You can specify more than one styles file or even a combination of `styles` and `styleUrls`.

When you use the `Angular` CLI command `ng g c` without the `--inline-style` flag, it creates an empty styles file for you and references that file in the component's generated `stylesUrls`.

```
ng g c hero-app
```

## Template Inline Styles:
You can embed `CSS` styles directly into the `HTML` template by putting them inside `<style>` tags.

```ts
@Component({
  selector: 'app-hero-controls',
  template: `
    <style>
      button {
        background-color: white;
        border: 1px solid #777;
      }
    </style>
    <h3>Tour of Heroes</h3>
    <button (click)="activate()">Activate</button>
  `
})
export class HeroAppComponent { }
```

## Template Link Tags:
You can also write `<link>` tags into the component's `HTML` template.

```ts
@Component({
  selector: 'app-hero-team',
  template: `
    <!-- We must use a relative URL so that the AOT compiler can find the stylesheet -->
    <link rel="stylesheet" href="../assets/hero-team.component.css">
    <h3>Team</h3>
    <ul>
      <li *ngFor="let member of hero.team">
        {{ member }}
      </li>
    </ul>
  `
})
export class HeroAppComponent { }
```

  > When building with the CLI, be sure to include the linked style file among the assets to be copied to the server as described in the [CLi wiki](https://github.com/angular/angular-cli/wiki/stories-asset-configuration). 
  >
  > Once included, the CLI will include the stylesheet, whether the link tag's href URL is relative to the application root or the component file.

## `CSS` `@imports`:
You can also import `CSS` files into the `CSS` files using the standard `CSS` `@import` rule.  For details, see `@import` on the [MDN](https://developer.mozilla.org/en-US/) site.

In this case, the URL is relative to the `CSS` file into which you're importing.

```css
/* The AOT compiler needs the './' to show that this is local */
@import './hero-details-box.css';
```

## External and Global Style Files:
When building with the CLI, you must configure the `angular.json` to include _all external assets_, including external style files.

Register **global** style files in the `styles` section which, by default, is pre-configured with the global `styles.css` file.

## Non-`CSS` Style Files:
If you're building with the CLI, you can write style files in `SASS`, `LESS`, or `stylus`, and specify those files in the `@Component.styleUrls` metadata with the appropriate extensions (`.scss`, `.less`, `.styl`) as in the following example:

```ts
@Component({
  selector: 'app-root',
  templateUrl: './app-component.html',
  styleUrls: ['./app.component.scss']
})
```

The CLI build process runs the pertinent `CSS` preprocessor.

When generating a component file with `ng g c`, the CLI emits an empty `CSS` styles file (`.css`) by default.  You can configure the CLI to default to your preferred `CSS` preprocessor as explaining in the [CLI wiki](https://github.com/angular/angular-cli/wiki/stories-asset-configuration).

  > Style `strings` added to the `@Component.styles` `array` _must be written in `CSS`_ because the CLI cannot apply a preprocessor to inline styles.

---

[Angular Docs](https://angular.io/guide/component-styles#loading-component-styles)