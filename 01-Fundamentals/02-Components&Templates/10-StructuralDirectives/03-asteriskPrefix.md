##### 2/10/2020
# Structural Directives - The Asterisk (`*`) Prefix
Surely you noticed the asterisk prefix to the directive name and wondered why it is necessary and what it does.

Here is `*ngIf` displaying the hero's name if `hero` exists:

```html
<div *ngIf="hero" class="name">{{ hero.name }}</div>
```

The asterisk is 'syntactic sugar' for something a bit more complicated.  Internally, `Angular` translates the `*ngIf` _attribute_ into an `<ng-template>` _element_, wrapped around the host element, like this:

```html
<ng-template [ngIf]="hero">
  <div class="name">{{ hero.name }}</div>
</ng-template>
```

  * The `*ngIf` directive moved to the `<ng-template>` element where it bames a property binding, `[ngIf]`
  * The rest of the `<div>`, including the class attribute, moved inside the `<ng-template>` element

The first form is not actually rendered, only the finished product ends up in the `DOM`.

![`ngIf` As Property Binding Inside `<ng-template>`](../../../Assets/ngIfInsideNgTemplate.png)

`Angular` consumed the `<ng-template>` content during its actual rendering and replaced the `<ng-template>` with a diagnostic comment.

The `NgFor` and `NgSwitch...` directives follow the same pattern.

---

[Angular Docs](https://angular.io/guide/structural-directives#the-asterisk--prefix)