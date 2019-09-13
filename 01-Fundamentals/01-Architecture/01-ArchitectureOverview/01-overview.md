##### 9/04/2019
# Architecture Overview
`Angular` is a platform and framework for building client applications in `HTML` and `TypeScript`.  `Angular` is written in `TypeScript`.  It implements core and optional functionality as a set of `TypeScript` libraries that you import into your apps.

The basic building blocks of an `Angular` application are **NgModules**, which provide a compilation context for **components**.  NgModules collect related code into functional sets; an `Angular` app is defined by a set of NgModules.  An app always has at least a _root module_ that enables **bootstrapping**, and typically has many more _feature modules_.

* Components define **views**, which are sets of screen elements that `Angular` can choose among and modify according to your program logic and data.
* Components use **services**, which provide specific functionality not directly related to views.  **Service providers** can be _injected_ into components as **dependencies**, making your code modular, reusable, and efficient.

Both components and services are simply `classes`, with **decorators** that mark their type and provide metadata that tells `Angular` how to use them.

* The metadata for a _component class_ associates it with a **template** that defines a view.  A template combines ordinary `HTML` with `Angular` **directives** and _binding markup_ that allows `Angular` to modify the `HTML` before rendering it for display.
* The metadata for a _service class_ provides the information `Angular` needs to make it available to components through **dependency injection** (DI).

An app's components typically define many views, arranged _hierarchically_.  `Angular` provides the **Router** service to help you define navigation paths among views.  The router provides sophisticated in-browser navigational capabilities.

---

[Angular Docs](https://angular.io/guide/architecture)