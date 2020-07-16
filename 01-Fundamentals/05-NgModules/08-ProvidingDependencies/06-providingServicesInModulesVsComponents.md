##### 7/09/2020
# Providing Dependencies - Providing Services in Modules vs. Components
Generally, provide services the whole app needs in the root module and scope services by providing them in lazy loaded modules.

The router works at the root level so if you put providers in a component, even `AppComponent`, lazy loaded modules, which rely on the router, can't see them.

Register a provider with a component when you must limit a service instance to a component and its component tree, that is, its child components. For example, a user editing component, `UserEditorComponent`, that needs a private copy of a caching `UserService` should register the `UserService` with the `UserEditorComponent`. Then each new instance of the `UserEditorComponent` gets its own cached service instance.

---

[Angular Docs](https://angular.io/guide/providers#providing-services-in-modules-vs-components)