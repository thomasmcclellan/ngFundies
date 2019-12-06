##### 11/27/2019
# Template Syntax - `SVG` in Templates
It is possible to use `SVG` as valid templates in `Angular`.  All of the template syntax below is applicable to both `SVG` and `HTML`.  

  > Learn more in the `SVG` [1.0](https://www.w3.org/TR/SVG11/) and [2.0](https://www.w3.org/TR/SVG2/) specifications.

Why would you sue `SVG` as template, instead of simply adding it as image to your application?

When you use an `SVG` as the template, you are able to use directives and bindings just like with `HTML` templates.  This means that you will be able to dynamically generate interactive graphics.

Refer to the sample code snippet below for a syntax example:

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-svg',
  templateUrl: './svg.component.svg',
  styleUrls: ['./svg.component.css']
})
export class SvgComponent {
  fillColor: string = 'rgb(255, 0, 0)'

  changeColor() {
    const r = Math.floor(Math.random() * 256)
    const g = Math.floor(Math.random() * 256)
    const b = Math.floor(Math.random() * 256)

    this.fillColor = `rgb(${r}, ${g}, ${b})'
  }
}
```

Add the following code to your `svg.component.svg` file:

```svg
<svg>
  <g>
    <rect
      x="0"
      y="0"
      width="100"
      height="100"
      [attr.fill]="fillColor"
      (click)="changeColor()"
    >
    <text
      x="120"
      y="50"
    >
      Click the rectangle to change the fill color
    </text>
  </g>
</svg>
```

Here, you can see the use of a `(click)` event binding and the property binding syntax (`[attr.fill]="fillColor"`).

---

[Angular Docs](https://angular.io/guide/template-syntax#svg-in-templates)