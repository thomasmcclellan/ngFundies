##### 2/17/2020
# Structural Directives - Prefer the Asterisk (`*`) Syntax
The asterisk syntax is more clear than the desugared form.  Use `<ng-container>` when there's no single element to host the directive.

While there's rarely a good reason to apply a structural directive in template _attribute_ or _element_ form, it's still important to known that `Angular` creates an `<ng-template>` and to understand how it works.  You'll refer to the `<ng-template>` when you write your own structural directives.

---

[Angular Docs](https://angular.io/guide/structural-directives#prefer-the-asterisk--syntax)