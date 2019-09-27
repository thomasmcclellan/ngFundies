##### 9/27/2019
# Introduction to Displaying Data - Showing an Array Property with `*ngFor`
To display a list of heroes, begin by adding an array of hero names to the component and redefine `myHero` to be the first name in the array.

`src/app/app.component.ts` (class):
```typescript
export class AppComponent {
  title: string = 'Tour of Heroes'
  heroes: string[] = ['Windstorm', 'Bombasto', 'Magneta', 'Tornado']
  myHero = this.heroes[0]
}
```

Now use the `Angular` `*ngFor` **directive** in the template to display each item in the `heroes` list.

`src/app/app.component.ts` (template):
```typescript
template: `
  <h1>{{ title }}</h1>
  <h2>My favorite hero is: {{ myHero }}</h2>
  <p>Heroes:</p>
  <ul>
    <li *ngFor="let hero of heroes">
      {{ hero }}
    </li>
  </ul>
`
```

This UI uses the `HTML` unordered list with `<ul>` and `<li>` tags.  The `*ngFor` in the `<li>` is the `Angular` _repeater_ directive.  It marks that `<li>` element (and its children) as the _repeater template_.

```html
<li *ngFor="let hero of heroes">
  {{ hero }}
</li>
```

  > **Notice**: the `hero` in the `*ngFor` double-quoted instruction; it is an example of a _template input variable_.  

`Angular` duplicates the `<li>` for each item in the list, setting the `hero` variable to the item (the hero) in the current iteration.  `Angular` uses that variable as the context for the interpolation in the double curly braces.

  > In this case, `*ngFor` is displaying an array, but it can repeat items for any [iterable](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols) object as well.

---

[Angular Docs](https://angular.io/guide/displaying-data)