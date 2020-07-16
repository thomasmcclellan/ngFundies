##### 6/23/2020
# Feature Modules - Importing a Feature Module
To incorporate the feature module into your app, you have to let the root module, `app.module.ts`, know about it.  Notice the `CustomerDashboardModule` export at the bottom of `customer-dashboard.module.ts`.  This exposes it so that other modules can get to it.  To import it into the `AppModule`, add it to the imports in `app.module.ts` and to the `imports` array:

```ts
import { HttpClientModule } from '@angular/common/http';
import { NgModule } from '@angular/core';
import { FormsModule } from '@angular/forms';
import { BrowserModule } from '@angular/platform-browser';
import { AppComponent } from './app.component';
import { CustomerDashboardModule } from './customer-dashboard/customer-dashboard.module';

@NgModule({
  declarations: [AppComponent],
  imports: [
    BrowserModule, 
    FormsModule,
    HttpClientModule,
    CustomerDashboardModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

Now the `AppModule` knows about the feature module.  If you were to add any service providers to the feature module, `AppModule` would know about those too, as would any other feature modules.  However, `NgModules` don't expose their components.

---

[Angular Docs](https://angular.io/guide/feature-modules#importing-a-feature-module)