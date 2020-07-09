##### 6/17/2020
# Entry Components - A Routed Entry Component
The second kind of entry component occurs in a route definition like this:

```ts
const routes: Routes = [
  {
    path: '',
    component: CustomerListComponent
  }
];
```

A route definition refers to a component by its type with component: `CustomerListComponent`.

All router components must be entry components. Because this would require you to add the component in two places (`router` and `entryComponents`) the `Compiler` is smart enough to recognize that this is a router definition and automatically add the `router` component into `entryComponents`.

---

[Angular Docs](https://angular.io/guide/entry-components#a-routed-entry-component)