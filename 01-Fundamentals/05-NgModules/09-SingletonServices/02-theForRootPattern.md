##### 7/14/2020
# Singleton Services - The `forRoot()` Pattern
Generally, you'll only need `providedIn` for providing services and `forRoot()`/`forChild()` for routing. However, understanding how `forRoot()` works to make sure a service is a singleton will inform your development at a deeper level.

If a module defines both `providers` and `declarations` (components, directives, pipes), then loading the module in multiple feature modules would duplicate the registration of the service. This could result in multiple service instances and the service would no longer behave as a singleton.

There are multiple ways to prevent this:
  * Use the `providedIn` syntax instead of registering the service in the module.
  * Separate your services into their own module.
  * Define `forRoot()` and `forChild()` methods in the module.

  > **NOTE**: There are two example apps where you can see this scenario; the more advanced `NgModules` live example, which contains `forRoot()` and `forChild()` in the routing modules and the `GreetingModule`, and the simpler Lazy Loading live example.

Use `forRoot()` to separate `providers` from a module so you can import that module into the root module with `providers` and child modules without `providers`.
  * Create a static method `forRoot()` on the module.
  * Place the `providers` into the `forRoot()` method.

```ts
static forRoot(config: UserServiceConfig): ModuleWithProviders<GreetingModule> {
  return {
    ngModule: GreetingModule,
    providers: [
      {provide: UserServiceConfig, useValue: config }
    ]
  };
}
```

## `forRoot()` and the `Router`:
`RouterModule` provides the `Router service, as well as router directives, such as `RouterOutlet` and `routerLink`.  The root application module imports `RouterModule` so that the application has a `Router` and the root application components can access the router directives.  Any feature modules must also import `RouterModule` so that their components can place router directives into their templates.

If the `RouterModule` didn't have `forRoot()` then each feature module would instantiate a new `Router` instance, which would break the application as there can only be one `Router`.  By using the `forRoot()` method, the root application module imports `RouterModule.forRoot()` and gets a `Router`, and all feature modules import `RouterModule.forChild()` which does not instantiate another `Router`.

  > **NOTE**: If you have a module which has both providers and declarations, you _can_ use this technique to separate them out and you may see this pattern in legacy apps.  However, since `Angular 6.0`, the best practice for providing services is with the `@Injectable()` `providedIn` property.

## How `forRoot()` Works:
`forRoot()` takes a service configuration `object` and returns a [ModuleWithProviders](https://angular.io/api/core/ModuleWithProviders), which is a simple `object` with the following properties:
  * `ngModule`: in this example, the `GreetingModule` class
  * `providers`: the configured providers

In this example the root `AppModule` imports the `GreetingModule` and adds the providers to the `AppModule` providers. Specifically, `Angular` accumulates all imported providers before appending the items listed in `@NgModule.providers`. This sequence ensures that whatever you add explicitly to the `AppModule` providers takes precedence over the providers of imported modules.

The sample app imports `GreetingModule` and uses its `forRoot()` method one time, in `AppModule`. Registering it once like this prevents multiple instances.

You can also add a `forRoot()` method in the `GreetingModule` that configures the greeting `UserService`.

In the following example, the optional, injected `UserServiceConfig` extends the greeting `UserService`. If a `UserServiceConfig` exists, the `UserService` sets the user name from that config.

```ts
constructor(@Optional() config?: UserServiceConfig) {
  if (config) this._userName = config.userName;
}
```

Here's `forRoot()` that takes a `UserServiceConfig` object:

```ts
static forRoot(config: UserServiceConfig): ModuleWithProviders<GreetingModule> {
  return {
    ngModule: GreetingModule,
    providers: [
      { provide: UserServiceConfig, useValue: config }
    ]
  };
}
```

Lastly, call it within the `imports` list of the `AppModule`.  In the following snippet, other parts of the file are left out.

```ts
import { GreetingModule } from './greeting/greeting.module';

@NgModule({
  imports: [
    GreetingModule.forRoot({ userName: 'Miss Marple' })
  ]
})
```

The app displays `'Miss Marple'` as the user instead of the default `'Sherlock Holmes'`.

Remember to import `GreetingModule` as a `JS` import at the top of the file and don't add it to more than one `@NgModule` `imports` list.

---

[Angular Docs](https://angular.io/guide/singleton-services#the-forroot-pattern)