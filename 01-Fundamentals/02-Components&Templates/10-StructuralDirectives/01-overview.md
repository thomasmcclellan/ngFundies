##### 2/06/2020
# Structural Directives - What Are Structural Directives?
Structural directives are responsible for `HTML` layout.  They shape or reshape the `DOM`'s _structure_, typically by adding, removing, or manipulating elements.

As with other directive, you apply a structural directive to a _host element_.  The directive then does whatever it's supposed to do with that host element and its descendants.

Structural directives are easy to recognize.  An asterisk (`*`) precedes the directive attribute name as in this example.

```html
<div
  *ngIf="hero"
  class="name"
>
  {{ hero.name }}
</div>
```

No brackets; no parentheses; just `*ngIf` set to a `string`.

You'll learn in this guide that the [asterisk is a convenience notation](https://angular.io/guide/structural-directives#asterisk) and the `string` is a [_microsyntax_](https://angular.io/guide/structural-directives#microsyntax), rather than the usual [template expression](https://angular.io/guide/template-syntax#template-expressions).  `Angular` desugars this notation into a marked-up `<ng-template>` that surrounds the host element and its descendents.  Each structural directive does something different with that template.

Three of the common, built-in structural directives--`NgIf`, `NgFor`, `NgSwitch`--are described in a previous section.

## Directive Spelling:
Throughout this guide, you'll see a directive spelled in both _PascalCase_ and _camelCase_.  Already, you've seen `NgIf` and `*ngIf`.  There's a reason.  `NgIf` refers to the directive _class_; `*ngIf` refers to the directive's _attribute name_.

A directive _class_ is spelled in _PascalCase_.  A directive's _attribute name_ is spelled in _camelCase_.  The guide refers to the directive _class_ when talking about its properties and what the directive does.  The guide refers to the _attribute name_ when describing how you apply the directive to an element int he `HTML` template.

  > There are two other kinds of `Angular` directives, described extensively elsewhere:
  >   1. Components
  >   2. Attribute Directives
  >
  > An _attribute directive_ changes the appearance or behavior of an element, component, or another directive.  For example, the built-in `NgStyle` directive changes several element styles at the same time.
  >
  > You can apply many _attribute_ directives to one host element.  You can **only apply one** _structural_ directive to a host element.

---

[Angular Docs](https://angular.io/guide/structural-directives)