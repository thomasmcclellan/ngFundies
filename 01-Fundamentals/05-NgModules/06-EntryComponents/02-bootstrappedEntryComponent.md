##### 6/16/2020
# Entry Components - A Bootstrapped Entry Component
The following is an example of specifying a bootstrapped component, `AppComponent`, in a basic `app.module.ts`:

```ts
@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    FormsModule,
    HttpClientModule,
    AppRoutingModule
  ],
  providers: [],
  bootstrap: [AppComponent] // bootstrapped entry component
})
```

A bootstrapped component is an entry component that `Angular` loads into the `DOM` during the bootstrap process (application launch). Other entry components are loaded dynamically by other means, such as with the router.

`Angular` loads a root `AppComponent` dynamically because it's listed by type in `@NgModule.bootstrap`.

A component can also be bootstrapped imperatively in the module's `ngDoBootstrap()` method. The `@NgModule.bootstrap` property tells the compiler that this is an entry component and it should generate code to bootstrap the application with this component.

A bootstrapped component is necessarily an entry component because bootstrapping is an imperative process, thus it needs to have an entry component.

---

[Angular Docs](https://angular.io/guide/entry-components#a-bootstrapped-entry-component)