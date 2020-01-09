##### 1/08/2020
# Dynamic Components - The Anchor Directive
Before you can add components you have to define an anchor point to tell `Angular` where to insert components.

The ad banner uses a helper directive called `AdDirective` to mark valid insertion points in the template.

```ts
import { Directive, ViewContainerRef } from '@angular/core';

@Directive({
  selector: '[ad-host]'
})
export class AdDirective {
  constructor(public viewContainerRef: ViewContainerRef) { }
}
```

`AdDirective` injects `ViewContainerRef` to gain access to the view container of the element that will host the dynamically added component.

In the `@Directive` decorator, notice the selector name, `ad-host`; that's what you use to apply the directive to the element.  The next section shows you how.

---

[Angular Docs](https://angular.io/guide/dynamic-component-loader#the-anchor-directive)