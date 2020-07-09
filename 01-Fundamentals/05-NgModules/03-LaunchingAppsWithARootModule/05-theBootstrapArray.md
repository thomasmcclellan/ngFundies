##### 6/08/2020
# Launching Apps with a Root Module - The `bootstrap` `Array`
The application launches by bootstrapping the root `AppModule`, which is also referred to as an `entryComponent`. Among other things, the bootstrapping process creates the component(s) listed in the `bootstrap` `array` and inserts each one into the browser `DOM`.

Each bootstrapped component is the base of its own tree of components. Inserting a bootstrapped component usually triggers a cascade of component creations that fill out that tree.

While you can put more than one component tree on a host web page, most applications have only one component tree and bootstrap a single root component.

This one root component is usually called `AppComponent` and is in the root module's `bootstrap` array.

---

[Angular Docs](https://angular.io/guide/bootstrapping#the-bootstrap-array)