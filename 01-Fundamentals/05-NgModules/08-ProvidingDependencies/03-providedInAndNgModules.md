##### 7/06/2020
# Providing Dependencies - `providedIn` and `NgModules`
It's also possible to specify that a service should be provided in a particular `@NgModule`.  For example, if you don't want `UserService` to be available to applications unless they import a `UserModule` you've created, you can specify that the service should be provided in the module:

```ts
import { Injectable } from '@angular/core';
import { UserModule } from './user.module';

@Injectable({
  providedIn: UserModule
})
export class UserService { }
```

The example above shows the preferred way to provide a service in a module.  This method is preferred because it enables tree-shaking of the service if nothing injects it.  If it's not possible to specify in the service which module should provide it, you can also declare a provider for the service within the module:

```ts
import { NgModule } from '@angular/core';
import { UserService } from './user.service';

@NgModule({
  providers: [UserService]
})
export class UserModule {
}
```

---

[Angular Docs](https://angular.io/guide/providers#providedin-and-ngmodules)