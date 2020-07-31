##### 7/27/2020
# NgModule API - Metadata
At a high level, `NgModules` are a way to organize `Angular` apps and they accomplish this through the metadata in the `@NgModule` decorator.  The metadata falls into three categories:
  1. **Static**: Compiler configuration which tells the compiler about directive selectors and where the templates the directives should be applied selector matching.  This is configured via the `declarations` array.
  2. **Runtime**: Injector configuration via the `providers` array.
  3. **Composability/Grouping**: Bringing `NgModules` together and making them available via the `imports` and `exports` arrays.

```ts
@NgModule({
  // Static, that is compiler configuration
  declarations: [], // Configure the selectors
  entryComponents: [], // Generate the host factory

  // Runtime, or injector configuration
  providers: [], // Runtime injector configuration

  // Composability / Grouping
  imports: [], // composing NgModules together
  exports: [] // making NgModules available to other parts of the app
})
```

---

[Angular Docs](https://angular.io/guide/ngmodule-api)