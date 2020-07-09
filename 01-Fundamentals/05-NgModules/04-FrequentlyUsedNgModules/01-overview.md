##### 6/09/2020
# Frequently-Used Modules - Overview
An `Angular` app needs at least one module that serves as the root module.  As you add features to your app, you can add them in modules.  The following are frequently used `Angular` modules with examples of some of the things they contain:

| `NgModule` | Import It From | Why You Use It |
|---|---|---|
| `BrowserModule` | `@angular/platform-browser` | When you want to run your app in a browser |
| `CommonModule` | `@angular/common` | When you want to use `NgIf`, `NgFor` |
| `FormsModule` | `@angular/forms` | When you want to build template driven forms (includes `NgModule`) |
| `ReactiveFormsModule` | `@angular/forms` | When you want to build reactive forms |
| `RouterModule` | `@angular/router` | When you want tou use `RouterLink`, `.forRoot()`, and `.forChild()` |
| `HttpClientModule` | `@angular/common/http` | When you want ot talk to a server |

---

[Angular Docs](https://angular.io/guide/frequent-ngmodules#frequently-used-modules)