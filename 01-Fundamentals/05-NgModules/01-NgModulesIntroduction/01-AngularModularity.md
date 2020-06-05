##### 5/29/2020
# NgModules Introduction - `Angular` Modularity
`NgModules` configure the injector and the compiler and help organize related things together.

An `NgModule` is a `class` marked by the `@NgModule` decorator.  `@NgModule` takes a metadata `object` that describes how to compile a component's template and how to create an injector at runtime.  It identifies the module's own components, directives, and pipes, making some of them public, through the `exports` property, so that external components can use them.  `@NgModule` can also add service providers to the application dependency injectors.

---

## `Angular` Modularity:
Modules are a great way to organize an application and extend it with capabilities from external libraries.

`Angular` libraries are `NgModules`, such as `FormsModule`, `HttpClientModule`, and `RouterModule`.  Many third-party libraries are available as `NgModules` such as Material Design, Ionic, and AngularFire2.

`NgModule` consolidate components, directives, and pipes into cohesive blocks of functionality, each focused on a feature area, application business domain, workflow, or common collection of utilities.

Modules can also add services to the applications. Such services might be internally developed, like something you'd develop yourself or come from outside sources, such as the `Angular` router and HTTP client.

Modules can be loaded eagerly when the application starts or lazy loaded asynchronously by the router.

`NgModule` metadata does the following:
  * Declares which components, directives, adn pipes belong to the module
  * Makes some of those components, directives, and pipe public so that other module's component templates can use them
  * Imports other modules with the components, directives, and pipes that components in the current module need
  * Provides services that the other application components can use

Every `Angular` app has at least one module, the root module.  You [bootstrap](https://angular.io/guide/bootstrapping) that module to launch the application.

The root module is all you need in a simple application  with a few components.  As the app grows, you refactor the root module into [feature modules](https://angular.io/guide/feature-modules) that represent collections of related functionality.  You then import these modules into the root module.

---

[Angular Docs](https://angular.io/guide/ngmodules)