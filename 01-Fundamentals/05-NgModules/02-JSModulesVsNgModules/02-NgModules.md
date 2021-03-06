##### 6/01/2020
# `JavaScript` Modules vs. `NgModules` - `NgModules`
The `Angular` CLI generates the following basic `AppModule` when creating a new app.

```js
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { AppComponent } from './app.component';

@NgModule({
  declarations: [AppComponent],
  imports: [BrowserModule],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule {}
```

At the top are the import statements.  The next section is where you configure the `@NgModule` by stating what components and directives belong to it (`declarations`) as well as which other modules it uses (`imports`).

---

[Angular Docs](https://angular.io/guide/ngmodules#the-basic-ngmodule)