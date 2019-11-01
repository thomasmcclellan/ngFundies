##### 11/01/2019
# Template Syntax - The `NgSwitch` Directives
`NgSwitch` is like the `JS` `switch` statement.  It displays one element from among several possible elements, based on a switch condition.  `Angular` puts only the selected element into the `DOM`.

`NgSwitch` is actually a set of three, cooperating directives: `NgSwitch`, `NgSwitchCase`, and `NgSwitchDefault` as in the following example:

```html
<div [ngSwitch]="currentItem.feature">
  <app-stout-item *ngSwitchCase="'stout'" [item]="currentItem"></app-stout-item>
  <app-device-item *ngSwitchCase="'slim'" [item]="currentItem"></app-device-item>
  <app-lost-item *ngSwitchCase="'vintage'" [item]="currentItem"></app-lost-item>
  <app-best-item *ngSwitchCase="'bright'" [item]="currentItem"></app-best-item>
  <!-- ... -->
  <app-unknown-item *ngSwitchDefault [item]="currentItem"></app-unknown-item>
</div>
```

![ngModel Demo](../../../Assets/ngSwitchDemo.gif)

`NgSwitch` is the controller directive.  Bind it to an expressio nthat returns the _switch value_, such as `feature`.  Though the `feature` value in this example is a `string`, the switch value can be of any type.

**Bind to** `[ngSwitch]`.  You'll get an error if you try to set `*ngSwitch` because `NgSwitch` is an _attribute_ directive, **NOT** a _structural_ directive.  Rather than touching the `DOM` directly, it changes the behavior of its companion directives.

**Bind to** `*ngSwitchCase` and `*ngSwitchDefault`.  The `NgSwitchCase` and `NgSwitchDefault` directives **ARE** _structural_ directives because they add/remove elements from the `DOM`.  
  * `NgSwitchCase` adds its elements to the `DOM` when its bound value equals the switch value and removes its bound value when it doesn't equal the switch value
  * `NgSwitchDefault` adds its element to the `DOM` when there is no selected `NgSwitchCase`

The switch directives are particularly useful for adding/removing _component elements_.  This example switches among four item components defined in the `item-switch.component.ts` file.  Each component has an item input property which is bound to the `currentItem` of the parent component.

Switch directives work as well with native elements and web components too.  For example, you could replace the `<app-best-item>` switch case with the following:

```html
<div *ngSwitchCase="'bright'">Are you as bright as {{ currentItem }}?</div>
```

---

[Angular Docs](https://angular.io/guide/template-syntax#the-ngswitch-directives)