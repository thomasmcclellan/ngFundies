##### 3/30/2020
# Template-Driven Forms - Revise `app.module.ts`
`app.module.ts` defines the application's root module.  In it youidentify the external modules you'll use in the application and declare the components that belong to this module, such as the `HeroFormComponent`.

Because template-driven forms are in their own module, you need to add the `FormsModule` to the `array` of `imports` for the application module before you can use forms.

Update it with the following:

```ts
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { FormsModule } from '@angular/forms';

import { AppComponent } from './app.component';
import { HeroFormComponent } from './her-form/hero-form.component';

@NgModule({
  imports: [
    BrowserModule,
    FormsModule
  ],
  declarations: [
    AppComponent,
    HeroFormComponent
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

  > There are two changes:
  >   1. You import `FormsModule`
  >   2. You add the `FormsModule` to the list of `imports` defined in the `@NgModule` decorator.  This gives the application access to all of the template-driven forms features, including `ngModule`

  > If a component, directive, or pipe belongs to a module in the `import` array, _don't_ redeclare it in the `declarations` array.  If you wrote it and it should belong to this module, _do_ declare it in the `declarations` array.

---

[Angular Docs](https://angular.io/guide/forms#revise-appmodulets)