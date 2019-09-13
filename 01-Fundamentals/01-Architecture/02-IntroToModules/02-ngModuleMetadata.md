##### 9/09/2019
# Introduction to Modules - NgModule Metadata
An **NgModule** is defined by a class decorated with `@NgModule()`.  The `@NgModule()` decorator is a function that takes a single metadata object, whose properties describe the module.  The most important properties are as follows:

| Property | Description |
|---|---|
| `imports` | Other modules whose exported classes are needed by component templates declared in _this_ NgModule |
| `providers` | Creators of **services** that this NgModule contributes to the global collection of services; they become accessible in all parts of the app (You can also specify providers at the component level, which is often preferred) |
| `declarations` | The **components**, **directives**, and **pipes** that belong to this NgModule | 
| `exports` | The subset of declarations that should be visible and usable in the _component templates_ of other NgModules |
| `bootstrap` | The main application view, called the _root component_, which hosts all other app views.  Only the _root NgModule_ should set the bootstrap property |

---

## Example:
```js
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';

@NgModule({
  imports: [ BrowserModule ],
  providers: [ Logger ],
  declarations: [ AppComponent ],
  exports: [ AppComponent ],
  bootstrap: [ AppComponent ]
})

export class AppModule { }
```

  > `AppComponent` is included in the `exports` list here for illustration; it isn't actually necessary in this example.  A root NgModule has no reason to _export_ anything because other modules don't need to _import_ the root NgModule.

---

[Angular Docs](https://angular.io/guide/architecture-modules)