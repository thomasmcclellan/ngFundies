##### 9/10/2019
# Introduction to Modules - NgModule and JS Modules
The **NgModule** system is different from and unrelated to the `JavaScript (ES2015)` module system for managing collections of `JavaScript` objects.  There are _complementary_ module systems that you can use together to write your apps.

In `JavaScript`, each _file_ is a module and all objects defined in the file belong to that module.  The module declares some objects to be public by marking them with an `export` keyword.  Other `JavaScript` modules use _import statements_ to access public objects from other modules.

```js
import { NgModule } from '@angular/core';
import { AppComponent } from './app.component';

...

export class AppModule { }
```

---

[Angular Docs](https://angular.io/guide/architecture-modules)