##### 2/04/2020
# Attribute Directives - Respond to User-Initiated Events
Currently, `appHighlight` simply sets an element color.  The directive could be more dynamic.  It could detect when the user mouses into our out of the element and respond by setting or clearing the highlight color.

Begin by adding `HostListener` to the list of imported symbols to `HighlightDirective`:

```ts
import { Directive, ElementRef, HostListener } from '@angular/core';
```

Then add two event handlers that respond when the mouse enters or leaves, each adorned by the `HostListener` decorator.

```ts
@HostListener('mouseenter') onMouseEnter() {
  this.highlight('yellow');
}

@HostListener('mouseleave') onMouseLeave() {
  this.highlight(null);
}

private highlight(color: string) {
  this.el.nativeElement.style.backgroundColor = color;
}
```

The `@HostListener` decorator lets you subscribe to events of the `DOM` element that hosts an attribute directive, the `<p>` in this case.

  > Of course you could reach into the `DOM` with standard `JS` and attach event listeners manually.  There are at least three problems with _that_ approach:
  >   1. You have to write the listener correctly
  >   2. The code must _detach_ the listener when the directive is destroyed to avoid memory leaks
  >   3. Talking to `DOM` API directly isn't a best practice

The handlers delegate to a helper method that sets the color on the host `DOM` element, `el`.

The helper method, `highlight`, was extracted from the constructor.  The revised constructor simply declares the injected `el: ElementRef`.

```ts
constructor(private el: ElementRef) { }
```

Here's the updated directive in full:

```ts
import { Directive, ElementRef, HostListener } from '@angular/core';

@Directive({
  selector: '[appHighlight]'
})
export class HighlightDirective {
  constructor(private el: ElementRef) { }

  @HostListener('mouseenter') onMouseEnter() {
    this.highlight('yellow');
  }

  @HostListener('mouseleave') onMouseLeave() {
    this.highlight(null);
  }

  private highlight(color: string) {
    this.el.nativeElement.style.backgroundColor = color;
  }
}
```

Run the app and confirm that the background color appears when you mouse hover over the `p` and disappears as it moves out.

![Mouse Move Directive](../../../Assets/mouseMoveDirectiveDemo.gif)

---

[Angular Docs](https://angular.io/guide/attribute-directives#respond-to-user-initiated-events)