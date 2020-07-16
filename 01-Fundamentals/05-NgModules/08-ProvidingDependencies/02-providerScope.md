##### 6/26/2020
# Providing Dependencies - Provider Scope
When you add a service provider to the root application injector, it's available throughout the app.  Additionally, these providers are also available to all the `classes` in the app as long they have the lookup token.

You should always provide your service in the root injector unless there is a case where you want the service to be available only if the consumer imports a particular `@NgModule`.

---

[Angular Docs](https://angular.io/guide/providers)