##### 7/28/2020
# `Angular` Dependency Injection - Overview
Dependency Injection (DI) is an important application design pattern.  `Angular` has its own DI framework, which is typically used in the design of `Angular` applications to increase their efficiency and modularity.

Dependencies are services or `objects` that a `class` needs to perform its `function`.  DI is a coding pattern in which a `class` asks for dependencies from external sources rather than creating them itself.

In `Angular`, the DI framework provides declared dependencies to a `class` is instantiated.  This guide explains how DI works in `Angular`, and how you use it to make your apps flexible, efficient, and robust, as well as testable and maintainable.

Start by reviewing this simplified version of the _heroes_ feature from the _Tour of Heroes_.  This simple version doesn't use DI; we'll walk through converting it to do so.

```ts
// heroes.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-heroes',
  template: `
    <h2>Heroes</h2>
    <app-hero-list></app-hero-list>
  `
})
export class HeroesComponent { }
```

```ts
// hero-list.component.ts
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

```ts
// hero.ts
export interface Hero {
  id: number;
  name: string;
  isSecret: boolean;
}
```

```ts
// mock-heroes.ts
import { Hero } from './hero';

export const HEROES: Hero[] = [
  { id: 11, isSecret: false, name: 'Dr Nice' },
  { id: 12, isSecret: false, name: 'Narco' },
  { id: 13, isSecret: false, name: 'Bombasto' },
  { id: 14, isSecret: false, name: 'Celeritas' },
  { id: 15, isSecret: false, name: 'Magneta' },
  { id: 16, isSecret: false, name: 'RubberMan' },
  { id: 17, isSecret: false, name: 'Dynama' },
  { id: 18, isSecret: true,  name: 'Dr IQ' },
  { id: 19, isSecret: true,  name: 'Magma' },
  { id: 20, isSecret: true,  name: 'Tornado' }
];
```

`HeroesComponent` is the top-level heroes component.  Its only purpose is to display `HeroListComponent`, which displays a list of hero names.

This version of the `HeroListComponent` gets heroes from the `HEROES` array, as in-memory collection defined in a separate `mock-heroes` file.

```ts
export class HeroListComponent {
  heroes = HEROES;
}
```

This approach works for prototyping, but is not robust or maintainable.  As soon as you try to test this component or get heroes from a remote server, you have to change the implementation of `HeroesListComponent` and replace every use of the `HEROES` mock data.

---

[Angular Docs](https://angular.io/guide/dependency-injection)