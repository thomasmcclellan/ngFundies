##### 7/21/2020
# Lazy Loading Feature Modules - `forRoot()` and `forChild()`
You might have noticed that the CLI adds `RouterModule.forRoot()` to the `AppRoutingModule` `imports` array.  This lets `Angular` know that the `AppRoutingModule` is a routing module and `forRoot()` specifies that this is the root routing module.  It configures all the routes you pass to it, gives you access to the router directives, and registers teh `Router` service.  Use `forRoot()` only once in your application, inside the `AppRoutingModule`.

The CLI also adds `RouterModule.forChild()` to feature routing modules.  This way, `Angular` knows that the route list is only responsible for providing additional routes and is intended for feature modules.  You can use `forChild()` in multiple modules.

The `forRoot()` method takes care of the _global_ injector configuration for the Router.  The `forChild()` method has no injector configuration.  It uses directives such as `RouterOutlet` and `RouterLink`.

---

[Angular Docs](https://angular.io/guide/lazy-loading-ngmodules#forroot-and-forchild)