##### 9/11/2019
# Introduction to Modules - Angular Libraries
`Angular` loads as a collection of `JS` modules.  You can think of them as _library modules_.  Each `Angular` library name begins with the `@angular` prefix.  Install them with the node package manager (`npm`) and import parts of them with `JS` `import` statements.

For example, import `Angular`'s `Component` decorator from the `@angular/core` library like this:
```typescript
import { Component } from '@angular/core';
```

You also import **NgModules** from `Angular` _libraries_ using `typescript` `import` statements.  For example, the following code imports the `BrowserModule` NgModule from the `platform-browser` library:
```typescript
import { BrowserModule } from '@angular/platform-browser';
```

In this example of the simple _root module_ above, the application module needs material from within `BrowserModule`.  To access that material, add it to the `@NgModule` metadata `imports` like this:
```typescript
imports: [ BrowserModule ],
```

In this way, you're using the `Angular` and `JS` module systems _together_.  Although it's easy to confuse the two systems, which share the common vocabulary of 'imports' and 'exports', you will become familiar with the different contexts in which they are used.

---

[Angular Docs](https://angular.io/guide/architecture-modules)