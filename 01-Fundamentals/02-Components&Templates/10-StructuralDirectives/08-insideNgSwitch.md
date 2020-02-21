##### 2/14/2020
# Structural Directives - Inside `NgSwitch` Directives
The `Angular` `NgSwitch` is actually a set of cooperating directives:  `NgSwitch`, `NgSwitchCase`, and `NgSwitchDefault`.

Here's an example:

```html
<div [ngSwitch]="hero?.emotion">
  <app-happy-hero 
    *ngSwitchCase="'happy'" 
    [hero]="hero"
  ></app-happy-hero>

  <app-sad-hero 
    *ngSwitchCase="'sad'" 
    [hero]="hero"
  ></app-sad-hero>

  <app-confused-hero 
    *ngSwitchCase="'confused'" 
    [hero]="hero"
  ></app-confused-hero>

  <app-unknown-hero 
    *ngSwitchDefault 
    [hero]="hero"
  ></app-unknown-hero>
</div>
```
The switch value assigned to `NgSwitch` (`hero.emotion`) determines which, if any, of the switch cases are displayed.

`NgSwitch` itself is _not_ a structural directive that controls the behavior of the other two switch directives.  That's why you write `[ngSwitch]`, **never** `*ngSwitch`.

`NgSwitchCase` and `NgSwitchDefault` _are_ structural directives.  You attach them to elements using the asterisk (`*`) prefix notation.  An `NgSwitchCase` displays its host element when its value matches the switch value.  The `NgSwitchDefault` displays its host when no sibling `NgSwitchCase` matches the switch value.

  > The element to which you apply a directive is its _host_ element.  The `<happy-hero>` is the host element for the happy `*ngSwitchCase`.  The `<unknown-hero>` is the host element for the `*ngSwitchDefault`.

As with other structural directives, the `NgSwitchCase` and `NgSwitchDefault` can be desugared into the `<ng-template>` element form:

```html
<div [ngSwitch]="hero?.emotion">
  <ng-template [ngSwitchCase]="'happy'">
    <app-happy-hero [hero]="hero"></app-happy-hero>
  </ng-template>

  <ng-template [ngSwitchCase]="'sad'">
    <app-sad-hero [hero]="hero"></app-sad-hero>
  </ng-template>

  <ng-template [ngSwitchCase]="'confused'">
    <app-confused-hero [hero]="hero"></app-confused-hero>
  </ng-template >
  
  <ng-template ngSwitchDefault>
    <app-unknown-hero [hero]="hero"></app-unknown-hero>
  </ng-template>
</div>
```

---

[Angular Docs](https://angular.io/guide/structural-directives#inside-ngswitch-directives)