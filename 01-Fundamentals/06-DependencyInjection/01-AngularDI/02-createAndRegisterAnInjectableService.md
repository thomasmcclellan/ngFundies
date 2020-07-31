##### 7/29/2020
# `Angular` Dependency Injection - Create and Register an Injectable Service
The DI framework lets you supply data to a component from an injectable service `class`, defined in its own file. To demonstrate, we'll create an injectable _service_ `class` that provides a list of heroes, and register that `class` as a provider of that service.

  > Having multiple `classes` in the same file can be confusing. We generally recommend that you define components and services in separate files.
  >
  > If you do combine a component and service in the same file, it is important to define the service first, and then the component. If you define the component before the service, you get a run-time `null` reference error.
  >
  > It is possible to define the component first with the help of the `forwardRef()` method as explained in this blog post.
  >
  > You can also use forward references to break circular dependencies.

## Create an Injectable Service `Class`:
The `Angular` CLI can generate a new `HeroService` class in the `src/app/heroes` folder with this command.

```
ng g s heroes/hero
```

The command creates the following `HeroService` skeleton.

```ts
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root',
})
export class HeroService {
  constructor() { }
}
```

The `@Injectable()` is an essential ingredient in every `Angular` service definition. The rest of the `class` has been written to expose a `getHeroes` method that returns the same mock data as before. (A real app would probably get its data asynchronously from a remote server, but we'll ignore that to focus on the mechanics of injecting the service.)

```ts
import { Injectable } from '@angular/core';
import { HEROES } from './mock-heroes';

@Injectable({
  // we declare that this service should be created
  // by the root application injector.
  providedIn: 'root',
})
export class HeroService {
  getHeroes() { return HEROES; }
}
```

## Configure an Injector with a Service Provider:
The `class` we have created provides a service. The `@Injectable()` decorator marks it as a service that can be injected, but `Angular` can't actually inject it anywhere until you configure an `Angular` dependency injector with a provider of that service.

The injector is responsible for creating service instances and injecting them into `classes` like `HeroListComponent`. You rarely create an `Angular` injector yourself. `Angular` creates injectors for you as it executes the app, starting with the root injector that it creates during the bootstrap process.

A provider tells an injector how to create the service. You must configure an injector with a provider before that injector can create a service (or provide any other kind of dependency).

A provider can be the service `class` itself, so that the injector can use new to create an instance. You might also define more than one `class` to provide the same service in different ways, and configure different injectors with different providers.

You can configure injectors with providers at different levels of your app, by setting a metadata value in one of three places:
  1. In the `@Injectable()` decorator for the service itself.
  2. In the `@NgModule()` decorator for an `NgModule`.
  3. In the `@Component()` decorator for a component.

The `@Injectable()` decorator has the `providedIn` metadata option, where you can specify the provider of the decorated service `class` with the root injector, or with the injector for a specific `NgModule`.

The `@NgModule()` and `@Component()` decorators have the providers metadata option, where you can configure providers for `NgModule`-level or component-level injectors.

---

[Angular Docs](https://angular.io/guide/dependency-injection#create-and-register-an-injectable-service)