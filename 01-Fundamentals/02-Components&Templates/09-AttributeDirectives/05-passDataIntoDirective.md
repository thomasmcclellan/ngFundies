##### 2/05/2020
# Attribute Directives - Pass Values Into the Directive with an `@Input` Data Binding
Currently the highlight color is hard-coded _within_ the directive.  That's inflexible.  In this section, you give the developer the power to set the highlight color while applying the directive.

Begin by adding `Input` to the list of symbols imported from `@angular/core`.

```ts
import { Directive, ElementRef, HostListener, Input } from '@angular/core';
```

Add a `highlightColor` property to the directive class like this:

```ts
@Input() highlightColor: string;
```

## Binding to an `@Input` Property:
Notice the `@Input` decorator.  It adds metadata to the class that makes the directive's `highlightColor` property available for binding.

It's called an _input_ property because data flows from the binding expression _into_ the directive.  Without that input metadata, `Angular` rejects the binding; see **08-summary.md** for more about that.

Try it by adding the following directive binding variations to the `AppComponent` template:

```html
<p appHighlight highlightColor="yellow">Highlighted in yellow</p>
<p appHighlight [highlightColor]="'orange'">Highlighted in orange</p>
```

Add a `color` property to the `AppComponent`.

```ts
export class AppComponent {
  color: string = 'yellow';
}
```

Let it control the highlight color with a property binding.

```html
<p appHighlight [highlightColor]="color">Highlighted with parent component's color</p>
```

That's good, but it would be nice to _simultaneously_ apply the directive and set the color _in the same attribute_ like this.

```html
<p [appHighlight]="color">Highlight me!</p>
```

The `[appHighlight]` attribute binding both applies the highlighting directive to the `<p>` element and sets the directive's highlight color with a property binding.  You're re-using the directive's attribute selector (`[appHighlight]`) to do both jobs.  That's crisp, compact syntax.

You'll have to remove the directive's `highlightColor` property to `appHighlight` because that's now the color property binding name.

```ts
@Input() appHighlight: string;
```

This is disagreeable.  The word, `appHighlight`, is a terrible property name and it doesn't convey the property's intent.

## Bind to an `@Input` Alias:
Fortunately you can name the directive property whatever you want _and **alias it**_ for binding purposes.

Restore the original property name and specify the selector as the alias in the argument to `@Input`.

```ts
@Input('appHighlight') highlightColor: string;
```

_Inside_ the directive the property is known as `highlightColor`.  _Outside_ the directive, where you bind to it, it's known as `appHighlight`.

You get the best of both worlds:  the property name you want and the binding syntax you want:

```html
<p [appHighlight]="color">Highlight me!</p>
```

Now that you're binding via the alias to the `highlightColor`, modify the `onMouseEnter()` method to use that property.  If someone neglects to bind to `appHighlight`, highlight the host element in red:

```ts
@HostListener('mouseenter') onMouseEnter() {
  this.highlight(this.highlightColor || 'red');
}
```

Here' the latest version of the directive class:

```ts
import { Directive, ElementRef, HostListener, Input } from '@angular/core';

@Directive({
  selector: '[appHighlight]'
})
export class HighlightDirective {
  @Input('appHighlight') highlightColor: string;

  @HostListener('mouseenter') onMouseEnter() : void {
    this.highlight(this.highlightColor || 'red');
  }

  @HostListener('mouseleave') onMouseLeave() : void {
    this.highlight(null);
  }

  constructor(private el: ElementRef) { }

  private highlight(color: string) : void {
    this.el.nativeElement.style.backgroundColor = color;
  }
}
```

---

[Angular Docs](https://angular.io/guide/attribute-directives#pass-values-into-the-directive-with-an-input-data-binding)