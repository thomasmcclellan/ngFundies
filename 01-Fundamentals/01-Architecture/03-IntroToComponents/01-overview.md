##### 9/12/2019
# Introduction to Components - Overview
A **component** controls a patch a screen called a **view**.

You define a component's application logic==what it does to support the view--inside a class.  The class interacts with the view through and API of properties and methods.

For example, `HeroListComponent` has a heroes property that holds an array of heroes.  Its `selectHero()` method sets a `selectedHero` property when the user clicks to choose a hero from that list.  The component acquires the heroes from a service, which is a `TypeScript` [parameter property](http://www.typescriptlang.org/docs/handbook/classes.html#parameter-properties) on the constructor.  The service is provided to the component through the **DI** system.

`src/app/hero-list.component.ts` (class):
```js
export class HeroListComponent implements OnInit {
  heroes: Hero[]
  selectedHero: Hero

  constructor(private service: HeroService) { }

  ngOnInit() {
    this.heroes = this.service.getHeroes()
  }

  selectedHero(hero: Hero): void {
    this.selectedHero = hero
  }
}
```

`Angular` creates, updates, and destroys components as the user moves through the application.  Your app can take action at each moment in this lifecycle through optional [lifecycle hooks](https://angular.io/guide/lifecycle-hooks), like `ngOnInit()`.

---

[Angular Docs](https://angular.io/guide/architecture-components)