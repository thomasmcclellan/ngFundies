##### 7/30/2020
# `Angular` Dependency Injection - Injecting Services
In order for `HeroListComponent` to get heroes from `HeroService`, it needs to ask for `HeroService` to be injected, rather than creating its own `HeroService` instance with new.

You can tell `Angular` to inject a dependency in a component's constructor by specifying a constructor parameter with the dependency type. Here's the `HeroListComponent` constructor, asking for the `HeroService` to be injected.

```ts
constructor(heroService: HeroService) { }
```

Of course, `HeroListComponent` should do something with the injected `HeroService`.  Here's the revised component, making use of the injected service, side-by-side with the previous version for comparison.

```ts
// hero-list.component.ts (with DI)
import { Component }   from '@angular/core';
import { Hero }        from './hero';
import { HeroService } from './hero.service';

@Component({
  selector: 'app-hero-list',
  template: `
    <div *ngFor="let hero of heroes">
      {{hero.id}} - {{hero.name}}
    </div>
  `
})
export class HeroListComponent {
  heroes: Hero[];

  constructor(heroService: HeroService) {
    this.heroes = heroService.getHeroes();
  }
}
```

```ts
// hero-list.component.ts (without DI)
import { Component }   from '@angular/core';
import { HEROES }      from './mock-heroes';

@Component({
  selector: 'app-hero-list',
  template: `
    <div *ngFor="let hero of heroes">
      {{hero.id}} - {{hero.name}}
    </div>
  `
})
export class HeroListComponent {
  heroes = HEROES;
}
```

`HeroService` must be provided in some parent injector. The code in `HeroListComponent` doesn't depend on where `HeroService` comes from. If you decided to provide `HeroService` in `AppModule`, `HeroListComponent` wouldn't change.

## Injector Hierarchy and Service Instances:
Services are singletons within the scope of an injector. That is, there is at most one instance of a service in a given injector.

There is only one root injector for an app. Providing `UserService` at the root or `AppModule` level means it is registered with the root injector. There is just one `UserService` instance in the entire app and every `class` that injects `UserService` gets this service instance unless you configure another provider with a child injector.

`Angular` DI has a hierarchical injection system, which means that nested injectors can create their own service instances. `Angular` regularly creates nested injectors. Whenever `Angular` creates a new instance of a component that has providers specified in `@Component()`, it also creates a new child injector for that instance. Similarly, when a new `NgModule` is lazy-loaded at run time, `Angular` can create an injector for it with its own providers.

Child modules and component injectors are independent of each other, and create their own separate instances of the provided services. When `Angular` destroys an `NgModule` or component instance, it also destroys that injector and that injector's service instances.

Thanks to injector inheritance, you can still inject application-wide services into these components. A component's injector is a child of its parent component's injector, and inherits from all ancestor injectors all the way back to the application's root injector. `Angular` can inject a service provided by any injector in that lineage.

For example, `Angular` can inject `HeroListComponent` with both the `HeroService` provided in `HeroComponent` and the `UserService` provided in `AppModule`.

---

[Angular Docs](https://angular.io/guide/dependency-injection#injecting-services)