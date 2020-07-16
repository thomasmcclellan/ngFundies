##### 6/22/2020
# Feature Modules - How to Make a Feature Module
Assuming you already have an app that you created with the `Angular` CLI, create a feature module using the CLI by entering the following command in the root project directory.  Replace `CustomerDashboard` with the name of your module.  You can omit the _Module_ suffix from the name because the CLI appends it:

```
ng generate module CustomerDashboard
```

This causes the CLI to create a folder called `customer-dashboard` with a file inside called `customer-dashboard.module.ts` with the following contents:

```ts
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';

@NgModule({
  imports: [
    CommonModule
  ],
  declarations: []
})
export class CustomerDashboardModule { }
```

The structure of an `NgModule` is the same whether it is a root module or a feature module.  In the CLI generated feature module, there are two `JS` import statements at the top of the file: the first imports `NgModule`, which, like the root module, lets you use the `@NgModule` decorator; the second imports `CommonModule`, which contributes many common directives such as `ngIf` or `ngFor`. Feature modules import `CommonModule` instead of `BrowserModule`, which is only imported once in the root module.  `CommonModule` only contains information for common directives such as `ngIf` and `ngFor` which are needed in most templates, whereas `BrowserModule` configures the `Angular` app for the browser which needs to be done only once.

The `declarations` array is available for you to add declarations, which are components, directives, and pipes that belong exclusively to this particular module.  To add a component, enter the following command line where `customer-dashboard` is the directory where the CLI generated the feature module and `CustomerDashboard` is the name of the component:

```
ng g c customer-dashboard/CustomerDashboard
```

This generates a folder for the new component within the `customer-dashboard` folder and updates the feature module with the `CustomerDashboardComponent` info:

```ts
import { CustomerDashboardComponent } from './customer-dashboard/customer-dashboard.component';

@NgModule({
  imports: [CommonModule],
  declarations: [CustomerDashboardComponent]
})
```

The `CustomerDashboardComponent` is now the `JS` import list at the top and added to the `declarations` array, which allows `Angular` to know to associate this new component with this feature module.

---

[Angular Docs](https://angular.io/guide/feature-modules#how-to-make-a-feature-module)