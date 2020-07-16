##### 7/16/2020
# Lazy Loading Feature Modules - Overview
By default, `NgModules` are eagerly loaded, which means that as soon as the app loads, so do all the `NgModules`, whether or not they are immediately necessary.  For large apps, with logs of routes, consider lazy-loading--a design pattern that loads `NgModules` as needed.  Lazy loading helps keep initial bundle sizes smaller, which in turn helps decrease load times.

## Lazy Loading Basics:
This section introduces the basic procedure for configuring a lazy-loaded route.  

To lazy load `Angular` modules, use `loadChildren` (instead of `component`) in your `AppRoutingModule` `routes` configuration as follows:

```ts
const routes: Routes = [
  {
    path: 'items',
    loadChildren: () => import('./items/items.module')
      .then(m => m.ItemsModule)
  }
];
```

In the lazy-loaded module's routing module, add a route for the component.

```ts
const routes: Routes = [
  {
    path: '',
    component: ItemsComponent
  }
];
```

Also be sure to remove the `ItemsModule` from the `AppModule`.

---

[Angular Docs](https://angular.io/guide/lazy-loading-ngmodules)