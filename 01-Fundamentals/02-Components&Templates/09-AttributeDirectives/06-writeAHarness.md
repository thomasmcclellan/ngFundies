##### 2/06/2020
# Attribute Directives - Write a Harness to Try It
It may be difficult to imagine how this directive actually works.  In this section, you'll turn `AppComponent` into a harness that lets you pick the highlight color with a radio button and bind your color choice to the directive.

Update `app.component.html` as follows:

```html
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
```

Revise the `AppComponent.color` so that it has no initial value.

```ts
export class AppComponent {
  color: string;
}
```

Here are the harness and directive in action:

![Directive Harness](../../../Assets/directiveHarnessDemo.gif)

---

[Angular Docs](https://angular.io/guide/attribute-directives#pass-values-into-the-directive-with-an-input-data-binding)