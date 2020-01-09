##### 12/31/2019
# Component Styles
`Angular` applications are styled with standard `CSS`.  That means that you can apply everything you know about `CSS` stylesheets, selectors, rules, media queries directly into `Angular` applications.

Additionally, `Angular` can bundle _component styles_ with components, enabling a more modular design than regular stylesheets.

## Using Component Styles
For every `Angular` component you write, you may define not only an `HTML` template, but also the `CSS` styles that go with that template, specifying any selectors, rules, and media queries that you need.

One way to do this is to set the `styles` property in the component metadata.  The `styles` property takes an `array` of `strings` that contain `CSS` code.  Usually you give it one `string`, as in the following example:

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

---

[Angular Docs](https://angular.io/guide/component-styles)