##### 7/13/2020
# Singleton Services - Providing a Singleton Service
There are two ways to make a service a singleton in `Angular`:
  1. Set the `providerIn` property of the `@Injectable()` to `'root'`
  2. Include the service in the `AppModule` or in a module that is only imported by the `AppModule`

## Using `providedIn`:
Beginning with `Angular 6.0`, the preferred way to create a singleton service is to set `providedIn` to `'root'` on the service's `@Injectable()` decorator. This tells `Angular` to provide the service in the application root.

```ts
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root'
})
export class UserService { }
```

## NgModule `providers` Array:
In apps built with `Angular` versions prior to `6.0`, services are registered `NgModule` providers `arrays` as follows:

```ts
@NgModule({
  providers: [UserService]
})
```

If this `NgModule` were the root `AppModule`, the `UserService` would be a singleton and available throughout the app. Though you may see it coded this way, using the `providedIn` property of the `@Injectable()` decorator on the service itself is preferable as of `Angular 6.0` as it makes your services tree-shakable.

---

[Angular Docs](https://angular.io/guide/singleton-services)