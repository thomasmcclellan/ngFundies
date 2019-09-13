##### 9/09/2019
# Introduction to Modules - Overview
`Angular` apps are modular and `Angular` has its own modularity system called **NgModules**.  NgModules are containers for a cohesive block of code dedicated to an application domain, a workflow, or a closely related set of capabilities.  They can contain components, service providers, or other code files whose scope is defined by the containing NgModule.  They can import functionality that is exported from other NgModules, and export selected functionality for use of other NgModules.

Every `Angular` app has at least one NgModule class, the _root module_, which is conventionally named `AppModule` and resides in a file named `app.module.ts`.  You launch your app by _bootstrapping_ the root NgModule.

  > While a small application might have only one NgModule, most apps have many more _feature modules_.  the _root_ NgModule for an app is so named because it can include child NgModules in a hierarchy of any depth.

---

[Angular Docs](https://angular.io/guide/architecture-modules)