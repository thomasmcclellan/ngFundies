##### 6/02/2020
# Launching Apps with a Root Module - Bootstrapping
An `NgModule` describes how the application parts fit together.  Every application has at least one `Angular` module, the _root_ module, which must be present for bootstrapping the application on launch.  By convention and by default, this `NgModule` is named `AppModule`.

When you use the `Angular` CLI command `ng new` to generate an app, the default `AppModule` is as follows:

```ts
/* JavaScript imports */
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { FormsModule } from '@angular/forms';
import { HttpClientModule } from '@angular/common/http';

import { AppComponent } from './app.component';

/* the AppModule class with the @NgModule decorator */
@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    FormsModule,
    HttpClientModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

After the import statements is a class with the `@NgModule` decorator.

The `@NgModule` decorator identifies `AppModule` as an `NgModule` class. `@NgModule` takes a metadata `object` that tells `Angular` how to compile and launch the application.
  * `declarations`: this application's lone component.
  * `imports`: import `BrowserModule` to have browser specific services such as `DOM` rendering, sanitization, and location.
  * `providers`: the service providers.
  * `bootstrap`: the root component that `Angular` creates and inserts into the index.`HTML` host web page.

The default application created by the `Angular` CLI only has one component, `AppComponent`, so it is in both the `declarations` and the `bootstrap` `arrays`.

---

[Angular Docs](https://angular.io/guide/ngmodules#the-basic-ngmodule)