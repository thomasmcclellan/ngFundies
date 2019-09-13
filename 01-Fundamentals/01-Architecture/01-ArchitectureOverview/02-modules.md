##### 9/05/2019
# Architecture Overview - Modules
`Angular` **NgModules** differs from and complement JS (ES5) modules.  An NgModule declares a compilation context for a set of components that is dedicated to an application domain, a workflow, or a closely related set of capabilities.  An NgModule can associate its components with related code, such as **services**, to form functional units.

Every `Angular` app has a _root module_, conventionally named `AppModule`, which provides the bootstrap mechanism that launches the application.  An app typically contains many functional modules.

  > Like JS modules, NgModules can import functionality from other NgModules, and allow their own functionality to be exported and used by other NgModules.  For example, to use the router service in your app, you import the **Router** NgModule.

Organizing your code into distinct functional modules helps in managing development of complex applications, and in designing for reusability.  In addition, this technique lets you take advantage of **lazy-loading**--that is, loading modules on demand--to minimize the amount of code that needs to be loaded at startup.

---

[Angular Docs](https://angular.io/guide/architecture)