##### 10/21/2019
# Template Syntax - Attribute, Class, and Style Bindings
The template syntax provides specialized one-way bindings for scenarios less well-suited to property binding.

## Attribute Binding:
Set the value of an attribute directly with an **attribute binding**.  This is the only exception to the rule that a binding sets a tart property and the only binding that creates and sets an attribute.

Usually, setting an element property with a property binding is preferable to setting the attribute with a `string`.  However, sometimes there is no element property to bind, so attribute binding is the solution.

Consider the [ARIA](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA) and [SVG](https://developer.mozilla.org/en-US/docs/Web/SVG).  They are purely attributes, don't correspond to element properties, and don't set element properties.  In these cases, there are no property targets to bind to.

Attribute binding syntax resembles property binding, but instead of an element property between brackets, start with the prefix `attr`, followed by a dot (`.`), and the name of the attribute.  You then set the attribute value, using an expression that resolves to a `string`, or remove the attribute when the expression resolves to `null`.

One of the primary use cases for attribute binding is to set ARIA attributes, as in this example:

`src/app/app.component.html`:
```html
<!-- Create and set an aria attribute for assistive technology -->
<button [attr.aria-label]="actionName">{{ actionName }} with Aria</button>
```

  > `colspan` and `colSpan`:
  > Notice the difference between the `colspan` and `colSpan` property.
  > 
  > If you wrote something like this:
  > ```html
  > <tr><td colspan="{{ 1 + 1 }}">Three-Four</td></tr>
  > ```
  > As the message says, the `<td>` element does not have a `colspan` property. This is true because `colspan` is an attribute--`colSpan` (with a capital `S`) is the corresponding property.  Interpolation and property binding can set only _properties_, not attributes.
  >
  > Instead, you'd use property binding and write it like this:
  > ```html
  > <!-- Notice the colSpan property is camelCase -->
  > <tr><td [colSpan]="1 + 1">Three-Four</td></tr>
  > ```

## Class Binding:
Add and remove `CSS` class names from an element's `class` attribute without a class binding.

Here's how to set the attribute without binding in plain `HTML`:
```html
<!-- Standard class attribute setting -->
<div class="item clearance special">Item clearance special</div>
```

Class binding syntax resembles property binding, but instead of an element property between brackets, start with the prefix `class`, optionally followed by a dot (`.`) and the name of a `CSS` class: `[class.class-name]`.

You can replace that with a binding to a `string` of the desired class names; this is an all-or-nothing, replacing binding.

```html
<h3>Overwrite all existing classes with a new class:</h3>
<div class="item clearance special" [att.class]="resetClasses">Reset all classes at once</div>
```

You can also add append a class to an element without overwriting the classes already on the element:

```html
<h3>Add a class:</h3>
<div class="item clearance special" [class.item-clearance]="itemClearance">Add another class</div>
```

Finally, you can bind to a specific class name.  `Angular` adds the class when the template expression evaluates to _truthy_.  It removes the class when the expression is _falsy_.

```html
<h3>Toggle the "special" class on/off with a property:</h3>
<div [class.special]="isSpecial">The class binding is special</div>

<h3>Binding to class.special overrides the class attribute:</h3>
<div class="special" [class.special]="!isSpecial">This one is not so special</div>

<h3>Using the bind- syntax:</h3>
<div bind-class.special="isSpecial">This class binding is special too</div>
```

While this technique is suitable for toggling a single class name, consider the `NgClass` directive when managing multiple class names at the same time.

## Style Binding:
You can set inline with a style binding.

Style binding syntax resembles property binding.  Instead of an element between brackets, start with the prefix `style`, followed by a dot (`.`) and the name of a `CSS` style property:  `[style.style.property]`.

```html
<button [style.color]="isSpecial ? 'red' : 'green'">Red</button>
<button [style.background-color]="canSave ? 'cyan' : 'grey'">Save</button>
```

Some style binding styles have a unit extension.  The following example conditionally sets the font size in 'em' and '%' units.

```html
<button [style.font-size.em]="isSpecial ? 3 : 1'">Red</button>
<button [style.font-size.%]="!isSpecial ? 150 : 50'">Small</button>
```

This technique is suitable for setting a single style, but consider the `NgStyle` directive when setting several inline styles at the same time.

  > **NOTE**: a _style property_ name can be written in either _kebab-case_ or _camelCase_.

---

[Angular Docs](https://angular.io/guide/template-syntax#attribute-class-and-style-bindings)