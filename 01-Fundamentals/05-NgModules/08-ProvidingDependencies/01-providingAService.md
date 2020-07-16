##### 6/25/2020
# Providing Dependencies - Providing a Service
If you already have an app that was created with the `Angular` CLI, you can create a service using the `ng g` CLI command in the root project directory.  Replace _User_ with the name of your service:

```
ng g s User
```

This command creates teh following `UserService` skeleton:

```ts
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root'
})
export class UserService { }
```

YOu can now inject `UserService` anywhere in your application.

The service itself is a `class` that the CLI generated and that' decorated with `@Injectable()`.  By default, this decorator has a `providedIn` property, which creates a provider for the service.  In this case, `providedIn: 'root'` specifies that `Angular` should provided the service in the root injector.

---

[Angular Docs](https://angular.io/guide/providers)