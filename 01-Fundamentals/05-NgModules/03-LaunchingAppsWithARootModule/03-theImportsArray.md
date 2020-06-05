##### 6/04/2020
# Launching Apps with a Root Module - The `imports` `Array`
The module's `imports` `array` appears exclusively in the `@NgModule` metadata `object`. It tells `Angular` about other `NgModules` that this particular module needs to function properly.

This list of modules are those that export components, directives, or pipes that the component templates in this module reference. In this case, the component is `AppComponent`, which references components, directives, or pipes in `BrowserModule`, `FormsModule`, or `HttpClientModule`. A component template can reference another component, directive, or pipe when the referenced `class` is declared in this module or the `class` was imported from another module.

---

[Angular Docs](https://angular.io/guide/bootstrapping#the-imports-array)