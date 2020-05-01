##### 4/28/2020
# Dynamic Forms - Bootstrap
Start by creating an `NgModule` called `AppModule`.

  > This cookbook uses Reactive Forms.

Reactive forms belong to a different `NgModule` called `ReactiveFormsModule`, so in order to access any reactive forms directives, you have to import `ReactiveFormsModule` from the `@angular/forms` library.

Bootstrap the `AppModule` in `main.ts`:

```ts
// app.module.ts
import { BrowserModule }                from '@angular/platform-browser';
import { ReactiveFormsModule }          from '@angular/forms';
import { NgModule }                     from '@angular/core';

import { AppComponent }                 from './app.component';
import { DynamicFormComponent }         from './dynamic-form.component';
import { DynamicFormQuestionComponent } from './dynamic-form-question.component';

@NgModule({
  imports: [ BrowserModule, ReactiveFormsModule ],
  declarations: [ AppComponent, DynamicFormComponent, DynamicFormQuestionComponent ],
  bootstrap: [ AppComponent ]
})
export class AppModule {
  constructor() {
  }
}
```

```ts
// main.ts
import { enableProdMode } from '@angular/core';
import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';

import { AppModule } from './app/app.module';
import { environment } from './environments/environment';

if (environment.production) {
  enableProdMode();
}

platformBrowserDynamic().bootstrapModule(AppModule);
```

---

[Angular Docs](https://angular.io/guide/dynamic-form#bootstrap)