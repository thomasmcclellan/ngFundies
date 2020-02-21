##### 2/06/2020
# Attribute Directives - Summary
The final source code follows:

```ts
// app.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html'
})
export class AppComponent {
  color: string;
}
```

```html
<!-- app.component.html -->
<h1>My First Attribute Directive</h1>
<h4>Pick a Highlight Color</h4>
<div>
  <input
    type="radio"
    name="colors"
    (click)="color='lightgreen'"
  >Green
  <input
    type="radio"
    name="colors"
    (click)="color='yellow'"
  >Yellow
  <input
    type="radio"
    name="colors"
    (click)="color='cyan'"
  >Cyan
</div>
<p [appHighlight]="color">Highlight Me!</p>
<p [appHighlight]="color" defaultColor="violet">Highlight Me Too!</p>
```

```ts
// highlight.directive.ts
// tslint:disable:member-ordering
import { Directive, ElementRef, HostListener, Input } from '@angular/core';

@Directive({
  selector: '[appHighlight]'
})
export class HighlightDirective {
  @Input('appHighlight') highlightColor: string;
  @Input() defaultColor: string;
  
  @HostListener('mouseenter') onMouseEnter() : void {
    this.highlight(this.highlightColor || this.defaultColor || 'red');
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

```ts
// app.module.ts
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';

import { AppComponent } from './app.component';
import { HighlightDirective } from './highlight.directive';

@NgModule({
  imports: [ BrowserModule ],
  declarations: [
    AppComponent,
    HighlightDirective
  ],
  bootstrap: [ AppComponent ]
})
export class AppModule { }
```

```ts
// main.ts
import { enableProdMode } from '@angular/core';
import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';

import { AppModule } from './app/app.module';
import { environment } from './environments/environment';

if (environment.production) enableProdMode();

platformBrowserDynamic().bootstrapModule(AppModule);
```

```html
<!-- index.html -->
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>Attribute Directives</title>
    <base href="/">
    <meta name="viewport" content="width=device-width, initial-scale=1">
  </head>
  <body>
    <app-root></app-root>
  </body>
</html>
```

You can also experience the [Attribute Directive Example](https://stackblitz.com/angular/qmrlvmxpkxx).

## Appendix: Why Add `@Input()`?:
In this demo, the `highlightColor` property is an _**input**_ property of the `HighlightDirective`.  You've seen it applied without an alias:

```ts
@Input() highlightColor: string;
```

You've seen it with an alias:

```ts
@Input('appHighlight') highlightColor: string;
```

Either way, the `@Input` decorator tells `Angular` that this property is _public_ and available for binding by a parent component.  Without `@Input`, `Angular` refuses to bind to the property.

You've bound template `HTML` to component properties before and never used `@Input`.  What's the difference?

The difference is a matter of trust.  `Angular` treats a component's template as _belonging_ to the component.  The component and its template trust each other implicitly.  Therefore, the component's own template may bind to _any_ property of that component, with or without the `@Input` decorator.

But a component or directive shouldn't blindly trust _other_ components/directives.  The property of a component or directive are hidden from binding by default.  They are _private_ from an `Angular` binding perspective.  When adorned with the `@Input` decorator, the property becomes _public_ from an `Angular` binding perspective.  Only then can it be bound by some other component or directive.

You can tell if `@Input` is needed by the position of the property name in a binding.
  * When it appears in the template expression to the _**right**_ of the equal sign, it belongs to the template's component and does not require the `@Input` decorator
  * When it appears in _**square brackets**_ to the right of the equal sign, the property belongs to some _other_ component/directive; that property must be adorned with the `@Input` decorator

Now apply that reasoning to the following example:

```html
<p [appHighlight]="color">Highlight Me!</p>
```

  * The `color` property in the expression on the right belongs to the template's component.  The template and its component trusts each other.  The `color` property doesn't require the `@Input` decorator
  * The `appHighlight` property on the left refers to an _aliased_ property of the `HighlightDirective`, not a property of the template's component.  There are trust issues.  Therefore, the directive property must carry the `@Input` decorator.

---

[Angular Docs](https://angular.io/guide/attribute-directives#summary)