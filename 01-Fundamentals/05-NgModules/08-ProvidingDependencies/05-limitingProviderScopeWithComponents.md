##### 7/08/2020
# Providing Dependencies - Limiting Provider Scope With Components
Another way to limit provider scope is by adding the service you want to limit to the component's providers `array`. Component providers and `NgModule` providers are independent of each other. This method is helpful when you want to eagerly load a module that needs a service all to itself. Providing a service in the component limits the service only to that component and its descendants. Other components in the same module can’t access it.

```ts
@Component({
  providers: [UserService]
})
```

---

[Angular Docs](https://angular.io/guide/providers#limiting-provider-scope-with-components)