##### 8/14/2020
# `Angular` Dependency Injection - Services That Need Other Services
Services can have their own dependencies.  `HeroService` is very simple and doesn't have any dependencies of its own.  Suppose, however, that you want it to report its activities through a logging service. You can apply the same _constructor injection_ pattern, adding a constructor that takes a `Logger` parameter.

Here is the revised `HeroService` that injects `Logger`, side by side with the previous service for comparison.

```ts
// hero.service.ts (v2)
import { Injectable } from '@angular/core';
import { HEROES }     from './mock-heroes';
import { Logger }     from '../logger.service';

@Injectable({
  providedIn: 'root',
})
export class HeroService {

  constructor(private logger: Logger) {  }

  getHeroes() {
    this.logger.log('Getting heroes ...');
    return HEROES;
  }
}
```

```ts
// hero.service.ts (v2)
import { Injectable } from '@angular/core';
import { HEROES }     from './mock-heroes';

@Injectable({
  providedIn: 'root',
})
export class HeroService {
  getHeroes() { return HEROES; }
}
```

```ts
// logger.service.ts
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root'
})
export class Logger {
  logs: string[] = []; // capture logs for testing

  log(message: string) {
    this.logs.push(message);
    console.log(message);
  }
}
```

The constructor asks for an injected instance of `Logger` and stores it in a private field called `logger`.  The `getHeroes()` method logs a message when asked to fetch heroes.

Notice that the `Logger` service also has the `@Injectable()` decorator, even though it might not need its own dependencies.  In fact, the `@Injectable()` decorator is **required for all services**.

When `Angular` creates a `class` whose constructor has parameters, it looks for type and injection metadata about those parameters so that it can inject the correct service.  If `Angular` can't find that parameter  information, it throws an error.  `Angular` can only find the parameter information _if the `class` has a decorator of some kind_.  The `@Injectable()` decorator is the standard decorator for service `classes`.

  > The decorator requirement is imposed by `TS`. `TS` normally discards parameter type information when it transpiles the code to `JS`. `TS` preserves this information if the `class` has a decorator and the `emitDecoratorMetadata` compiler option is set true in `TS`'s `tsconfig.json` configuration file. The CLI configures `tsconfig.json` with `emitDecoratorMetadata: true`.
  >
  > **This means you're responsible for putting `@Injectable()` on your service `classes`**.

## Dependency Injection Tokens:
When you configure an injector with a provider, you associate that provider with a [DI token](https://angular.io/guide/glossary#di-token). The injector maintains an internal _token-provider_ map that it references when asked for a dependency. The token is the key to the map.

In simple examples, the dependency value is an instance, and the `class` type serves as its own lookup key. Here you get a `HeroService` directly from the injector by supplying the `HeroService` type as the token:

```ts
heroService: HeroService;
```

The behavior is similar when you write a constructor that requires an injected `class`-based dependency. When you define a constructor parameter with the `HeroService` `class` type, `Angular` knows to inject the service associated with that `HeroService` `class` token:

```ts
constructor(heroService: HeroService)
```

## Optional Dependencies:
`HeroService` _requires_ a logger, but what if it could get by without one?

When a component or service declares a dependency, the `class` constructor takes that dependency as a parameter. You can tell `Angular` that the dependency is optional by annotating the constructor parameter with `@Optional()`.

```ts
import { Optional } from '@angular/core';

...

constructor(@Optional() private logger?: Logger) {
  if (this.logger) this.logger.log(someMessage);
}
```

When using `@Optional()`, your code must be prepared for a `null` value. If you don't register a logger provider anywhere, the injector sets the value of `logger` to `null`.

  > `@Inject()` and `@Optional()` are parameter decorators. They alter the way the DI framework provides a dependency, by annotating the dependency parameter on the constructor of the `class` that requires the dependency.
  >
  > Learn more about parameter decorators in [Hierarchical Dependency Injectors](https://angular.io/guide/hierarchical-dependency-injection).

---

[Angular Docs](https://angular.io/guide/dependency-injection#services-that-need-other-services)