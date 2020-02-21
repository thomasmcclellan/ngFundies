##### 2/20/2020
# Structural Directives - Write a Structural Directive
In this section, you write an `UnlessDirective` structural directive that does the opposite of `NgIf`.  `NgIf` displays the template content when the condition is `true`.  `UnlessDirective` displays the content when the condition is **`false`**.

```html
<p *appUnless="condition">Show this sentence unless the condition is true.</p>
```

Creating a directive is similar to creating a component.
  * Import the `Directive` decorator (instead of the `Component` decorator)
  * Import the `Input`, `TemplateRef`, and `ViewContainerRef` symbols; you'll need them for _any_ structural directive
  * Apply the decorator to the directive class
  * Set the `CSS` _attribute selector_ that identifies the directive when applied to an element in a template

Here's how you might begin:

```ts
import { Directive, Input, TemplateRef, ViewContainerRef } from '@angular/core';

@Directive({
  selector: '[appUnless]'
})
export class UnlessDirective {

}
```

The directive's _selector_ is typically the directive's **attribute name** in square brackets, `[appUnless]`.  The brackets define a `CSS` _attribute selector`.

The directive _attribute name_ should be spelled in **_lowerCaseCamel_** and begin with a prefix.  **Don't use `ng`**; that prefix belongs to `Angular`.  Pick something short that fits you or your company.  In this example, the prefix is `app`.

The directive _class_ name ends with `Directive`, per the [style guide](https://angular.io/guide/styleguide#02-03).  `Angular`'s own directives do not.

## TemplateRef and ViewContainerRef:
A simple structural directive like this one creates an [embedded view](https://angular.io/api/core/EmbeddedViewRef) from the `Angular`-generated `<ng-template>` and inserts that view in a [view container](https://angular.io/api/core/ViewContainerRef) adjacent to the directive's original `<p>` host element.

You'll acquire the `<ng-template>` contents with a `TemplateRef` and access the _view container_ through the `ViewContainerRef`.

You inject both in the directive constructor as private variables of the class.

```ts
constructor(
  private templateRef: TemplateRef<any>,
  private viewContainer: ViewContainerRef
) { }
```

## The `appUnless` Property:
The directive consumer expects to bind a `true`/`false` condition to `[appUnless]`.  That means the directive needs an `appUnless` property, decorated with `@Input()`.

```ts
@Input() set appUnless(condition: boolean) : void {
  if (!condition && !this.hasView) {
    this.viewContainer.createdEmbeddedView(this.templateRef);
    this.hasView = true;
  } else if (condition && this.hasView) {
    this.viewContainer.clear();
    this.hasView = false;
  }
}
```

`Angular` sets the `appUnless` property whenever the value of the condition changes.  Because the `appUnless` property does work, it needs a setter.
  * If the condition is _falsy_ and the view hasn't been created previously, tell the _view container_ to created the _embedded view_ from the template
  * If the condition is _truthy_ and the view is currently displayed, clear the container which also destroys the view

Nobody reads the `appUnless` property do it doesn't need a getter.

The completed directive code looks like this:

```ts
import { Directive, Input, TemplateRef, ViewContainerRef } from '@angular/core';

// Add the template content to the DOM unless the condition is true.
@Directive({ selector: '[appUnless]' })
export class UnlessDirective {
  private hasView: boolean = false;

  constructor(
    private templateRef: TemplateRef,
    private viewContainer: ViewContainerRef
  ) { }

  @Input() set appUnless(condition: boolean) : void {
    if (!condition && !this.hasView) {
      this.viewContainer.createEmbeddedView(this.templateRef);
      this.hasView = true;
    } else if (condition && this.hasView) {
      this.viewContainer.clear();
      this.hasView = false;
    }
  }
}
```

Add this directive to the `declarations` `array` of the `AppModule`.

Then create some `HTML` to try it.

```html
<p
  *appUnless="condition"
  class="unless a"
>
  (A) This paragraph is displayed because the condition is false.
</p>
<p
  *appUnless="!condition"
  class="unless b"
>
  (B) Although this condition is true, this paragraph is displayed because appUnless is set to false.
</p>
```

when the `condition` is _falsy_, the top (A) paragraph appears and the bottom (B) disappears.  When the `condition` is _truthy_, the two alternate.

![Custom Directive](../../../Assets/customDirectiveDemo.gif)

---

[Angular Docs](https://angular.io/guide/structural-directives#write-a-structural-directive)