##### 1/22/2020
# Attribute Directives - Build A Simple Attribute Directive
An attribute directive minimally requires building a controller class annotated with `@Directive`, which specifies the selector that identifies the attribute.  The controller class implements the desired directive behavior.

This page demonstrates building a simple `appHighlight` attribute directive to set an element's background color when the user hovers over that element.  You can apply it like this:

```html
<p appHighlight>Highlight me!</p>
```

Please note that directives `do not` support namespaces.

```html
<p app:Highlight>This is invalid</p>
```

## Write The Directive Code:
Create the directive class file in a terminal window with the CLI command `ng generate directive` (or `ng g d`).

```
ng g d highlight
```

The CLI creates `src/app/highlight.directive.ts`, a corresponding test file `src/app/highlight.directive.spec.ts`, and _declares_ the directive class in the root `AppModule`.

  > _Directives_ must be declared in `Angular` Modules in the same manner as _components_.

The generated `src/app/highlight.directive.ts` is as follows:

```ts
import { Directive } from '@angular/core';

@Directive({
  selector: '[appHighlight]'
})
export class HighlightDirective {
  constructor() { }
}
```

The imported `Directive` symbol provides `Angular` the `@Directive` decorator.

The `@Directive` decorator's lone configuration property specifies the directive's [`CSS` attribute selector](https://developer.mozilla.org/en-US/docs/Web/CSS/Attribute_selectors), `[appHighlight]`.

It's the brackets (`[]`) that make it an attribute selector.  `Angular` locates each element in the templates that has an attribute named `appHighlight` and applies the logic of this directive to that element.

The _attribute selector_ pattern explains the name of this kind of directive.

  > **Why not 'highlight'?**
  >
  > Though _highlight_ would be a more concise selector than `appHighlight` and it would work, the best practice is to prefix selector names to ensure they don't conflict with standard `HTML` attributes.  This also reduces the risk of colliding with third-party directive names.  The CLI added the `app` prefix for you.
  >
  > Make sure you do **not** prefix the `highlight` directive name with `ng` because that prefix is reserved for `Angular` and using it could cause bugs that are difficult to diagnose.

After the `@Directive` metadata comes the directive's controller class, called `HighlightDirective`, which contains the (currently empty) logic for the directive.  Exporting `HighlightDirective` makes the directive accessible.

Now edit the generated `src/app/highlight.directive.ts` to look as follows:

```ts
import { Directive, ElementRef } from '@angular/core';

@Directive({
  selector: '[appHighlight]'
}) 
export class HighlightDirective {
  constructor(el: ElementRef) {
    el.nativeElement.style.backgroundColor = 'yellow'
  }
}
```

The `import` statement specifies an additional `ElementRef` symbol from the `Angular` `core` library:

you use the `ElementRef` in the directive's constructor to inject a reference to the host `DOM` element, the element to which you applied `appHighlight`.

`ElementRef` grants direct access to the host `DOM` element through its `nativeElement` property.

This first implementation sets teh background color of the host element to yellow.

---

[Angular Docs](https://angular.io/guide/attribute-directives#build-a-simple-attribute-directive)