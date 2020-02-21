##### 2/13/2020
# Structural Directives - One Structural Directive Per Host Element
Someday you'll want to repeat a block of `HTML` but only when a particular condition is `true`.  You'll _try_ to put both an `*ngFor` and an `*ngIf` on the same host element.  `Angular` won't let you.  You may apply only one _structural_ directive to an element.

The reason is simplicity.  Structural directive can do complex things with the host element and is descendents.  When two directives lay claim to the same host element, which one takes precedence?  Which should go first, the `NgIf` or the `NgFor`?  Can the `NgIf` cancel the effect of the `NgFor`?   If so (and it seems lik it should be so), how should `Angular` generalize the ability to cancel for other structural directives?

There are no easy answers to these questions.  Prohibiting multiple structural directives makes them moot.  There's an easy solution for this use case:  put the `*ngIf` on a container element that wraps the `*ngFor` element.  One or both elements can be an `ng-container` so you don't have to introduce extra levels of `HTML`.

---

[Angular Docs](https://angular.io/guide/structural-directives#one-structural-directive-per-host-element)