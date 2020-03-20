##### 2/25/2020
# Pipes - Pipes and Change Detection
`Angular` looks for changes to data-bound values through a _change detection_ process that runs after every `DOM` event: event keystroke, mouse move, and server response.  This could be expensive.  `Angular` strives to lower the cost whatever possible and appropriate.

`Angular` picks a simpler, faster change detection algorithm when you use a pipe.

## No Pipe:
In the next example, the component uses the default, aggressive change detection strategy to monitor and update its display of every hero in the `heroes` array.  Here's the template:

```html
New hero:
  <input 
    type="text"
    #box
    (keyup.enter)="addHero(box.value); box.value=''"
    placeholder="hero name"
  >
  <button (click)="reset()">Reset</button>
  <div *ngFor="let hero of heroes">
    {{ hero.name }}
  </div>
```

The companion component class provides heroes, adds heroes into the `array`, and can reset the `array`.

```ts
export class FlyingHeroesComponent {
  heroes: any[] = [];
  canFly: boolean = true;

  constructor() { }

  addHero(name: string) : void {
    name = name.trim();
    
    if (!name) return;

    let hero = {name, canFly: this.canFly};
    this.heroes.push(hero);
  }

  reset() { this.heroes = HEROES.slice(); }
}
```

You can add heroes and `Angular` updates the display when you do.  If you click the `reset` button, `Angular` replaces `heroes` with a new `array` of the original heroes and updates the display.  If you added the ability to remove or change a hero, `Angular` would detect those changes nad update the display as well.

## `FlyingHeroesPipe`:
Add a `FlyingHeroesPipe` to the `*ngFor` repeater that filters the list of heroes to just those heroes who can fly.

```html
<div *ngFor="let hero of (heroes | flyingHeroes)">
  {{ hero.name }}
</div>
```

Here's the `FlyingHeroesPipe` implementation, which follows the pattern for custom pipes described earlier.

```ts
import { Pipe, PipeTransform } from '@angular/core';
import { Flyer } from './heroes';

@Pipe({ name: 'flyingHeroes' })
export class FlyingHeroesPipe implements PipeTransform {
  transform(allHeroes: Flyer[]) : Flyer[] {
    return allHeroes.filter(hero => hero.canFly);
  }
}
```

Notice the odd behavior in the [live example](https://stackblitz.com/angular/njnorvdmvvx?file=src%2Fapp%2Fapp.component.html): when you add flying heroes, none of them are displayed under "Heroes who fly".

Although you're not getting the behavior you want, `Angular` isn't broken. It's just using a different change-detection algorithm that ignores changes to the list or any of its items.

Notice how hero is added:

```ts
this.heroes.push(hero);
```

You add the hero into the `heroes` `array`.  The reference to the `array` hasn't changed.  It's the same `array`.  That's all `Angular` cares about.  From its perspective, _same `array`, no change, no display update_.

To fix that, create an `array` with the new hero appended and assign that to heroes.  This time `Angular` detects that the `array` reference has changed.  It executes the pipe adn updates the displays with the new `array`, which includes the new flying hero.

If you _mutate_ the `array`, no pipe is invoked and the display isn't updated; if you _replace_ the `array`, the pipe executes and the display is updated.  The Flying Heroes application extends the code with checkbox switches and additional displays to help you experience these effects.

![Change Detection](../../../Assets/changeDetectionDemo.gif)

Replace the `array` is an efficient way to signal `Angular` to update to display.  When do you replace the `array`?  When the data changes. That's an easy rule to follow in _this_ example where the only way to change the data is by adding a hero.

More often, you don't know when the data has changed, especially is applications that mutate data in many ways, perhaps in application location far away.  A component in such an application usually can't know about those changes.  Moreover, it's unwise to distort the component design to accommodate a pipe.  Strive to keep the component class independent of the `HTML`.  The component should be unaware of pipes.

For filtering flying heroes, consider an _impure pipe_.
  
---

[Angular Docs](https://angular.io/guide/pipes#pipes-and-change-detection)