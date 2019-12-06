##### 11/26/2019
# Template Syntax - Built-In Template Functions
## The `$any()` Type Cast Function:
Sometimes a binding expression triggers a type error during [AOT compilation](https://angular.io/guide/aot-compiler) and it is not possible or difficult to fully specify the type.  To silence the error, you can use the `$any()` cast `function` to cast the expression to the `any` type as in the following example:

```html
<p>The item's undeclared best by date is: {{ $any(item).bestByDate }}</p>
```

When the `Angular` compiler turns this template into `TS` code, it prevents `TS` fom reporting that `bestByDate` is not a member of the `item` `object` when it runs type checking on the template.

The `$any()` cast `function` also works with `this` to allow to undeclared members of the component.

```html
<p>The item's undeclared best by date is: {{ $any(this).bestByDate }}</p>
```

The `$any()` cast `function` works anywhere in a binding expression where a method call is valid.

---

[Angular Docs](https://angular.io/guide/template-syntax#built-in-template-functions)