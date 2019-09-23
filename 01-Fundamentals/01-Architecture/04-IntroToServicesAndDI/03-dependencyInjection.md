##### 9/20/2019
# Introduction to Services and Dependency Injection - Dependency Injection (DI)
**DI** is wired into the `Angular` framework and used everywhere to provide new components with the services or other things they need.  Components consume services; that is, you can _inject_ a service into a component, giving the component access to that service class.

To define a class as a service in `Angular`, use the `@Injectable()` decorator to provide the metadata that allows `Angular` to inject it into a component as a _dependency_.  

  * The _injector_ is the main mechanism.  `Angular` creates an application-wide injector for you during the _bootstrap_ process, and, additional injectors as needed.  You don't have to create injectors.
  * An injector creates dependencies, and maintains a _container_ of dependency instances that it reuses if possible.
  * A _provider_ is an object that tells an injector how to obtain or create a dependency.

For any dependency that you need in your app, you must register a provider with the app's injector, so that the injector can use the provider to create new instances.  For a service, the provider is typically the service class itself.

  > A dependency doesn't have to be a service--it could be a function, for example, or a value.

When `Angular` creates a new instance of a component class, it determines which services or other dependencies that component needs y looking at the constructor parameter types.  For example, the constructor of `HeroListComponent` needs `HeroService`.

`src/app/hero-list.component.ts` (constructor):
```js
constructor(private service: HeroService) { }
```

  > When `Angular` discovers that a component depends on a service, it first checks if the injector has any existing instances of that service.  If a requested service instance doesn't yet exist, the injector makes one using the registered provider, and adds it to the injector before returning the service to `Angular`.

  > When all requested services have been resolved and returned, `Angular` can call the component's constructor with those services as arguments.

## Providing Services:
You must register at least one _provider_ of any service you are going to use.  The provider can be part of the service's own metadata, making that service available everywhere, or you can register providers with specific modules or components.  You register providers in the metadata of the service (in the `@Injectable()` decorator), or in the `@NgModule()` or `@Component()` metadata.

  > By default, the `Angular CLI` command `ng generate service` registers a provider with the root injector for your service by including provider metadata in the `@Injectable()` decorator.  The tutorial uses this method to register the provider of `HeroService` class definition.
  >
  > ```js
  > @Injectable({
  >   providedIn: 'root'
  > })
  > ```
  >
  > When you provide the service at the root level, `Angular` creates a single, shared instance of `HeroService` and injects it into any class that asks for it.  Registering the provider in the `@Injectable()` metadata also allows `Angular` to optimize an app by removing the service from the compiled app if it isn't used.

  > When you register a provider with a specific NgModule, the same instance of a service is available to all components in that NgModule.  To register at this level, use the providers property of the `@NgModule()` decorator.
  > 
  > ```js
  > @NgModule({
  >   providers: [
  >     BackendService,
  >     Logger
  >   ],
  >   ...
  > })

  > When you register a provider at the component level, you get a new instance of the service with each new instance of that component.  At the component level, register a service provider in the `providers` property of the `@Component()` metadata.
  >
  > ```js
  > @Component({
  >   selector: 'app-hero-list',
  >   templateUrl: './hero-list.component.html',
  >   providers: [ HeroService ]
  > })
  > ```

---

[Angular Docs](https://angular.io/guide/architecture-services)