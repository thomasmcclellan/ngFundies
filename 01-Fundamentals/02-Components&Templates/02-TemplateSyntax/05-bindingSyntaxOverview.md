##### 10/07/2019
# Template Syntax - Binding Syntax: An Overview
**Data-binding** is a mechanism for coordinating what users see, specifically with application data values.  While you could push values to and pull values from `HTML`, the application is easier to write, read, and maintain if you turn these tasks over to a binding framework.  You simply declare bindings between binding sources, target `HTML` elements, and let the framework do the rest.

`Angular` provides many kinds of data-binding.  Binding types can be grouped into three categories distinguished by the direction of data flow:
  * From the _source-to-view_
  * From _view-to-source_
  * Two-way sequence: _view-to-source-to-view_

| Type | Syntax | Category |
|---|---|---|
| Interpolation<br>Property<br>Attribute<br>Class<br>Style | <pre>{{ expression }}<br>[target]="expression"<br>bind-target="expression`</pre> | One-way from data source to view target |
| Event | <pre>(target)="statement<br>on-target="statement"</pre> | One-way from view target to data source |
| Two-way | <pre>[(target)]="expression"<br>bindon-target="expression"</pre> | Two-way |

Binding types other than interpolation have a _target name_ to the left of the equal sign, either surrounded by punctuation, `[]` or `()`, or preceded by a prefix: `bind-`, `on-`, `bindon-`.

The _target_ of a binding is the property or event inside the binding punctuation: `[]`, `()`, or `[()]`.

Every public member of a _source_ directive is automatically available for binding.  You don't have to do anything special to access a directive member in a template expression or statement.

## Data-Binding and `HTML`:
In the normal course of `HTML` development, you create a visual structure with `HTML` elements, and you modify those elements by setting element attributes with `string` constants.

```html
<div class="special">Plain old HTML</div>
<img src="images/item.png">
<button disabled>Save</button>
```

With data-binding, you can control things like the state of a button:

`src/app/app.component.html`:
```html
<!-- Bind button disabled state to 'isUnchanged' property -->
<button [disabled]="isUnchanged">Save</button>
```

  > **NOTE**: the binding is to the `disabled` property of the button's `DOM` element, _not_ the attribute.  This applies to data-binding in general.  Data-binding works with _properties_ of `DOM` elements, components, and directives; not `HTML` _attributes_.

## `HTML` Attribute vs. `DOM` Property:
The distinction between an `HTML` attribute and a `DOM` property is key to understanding how `Angular` binding works.  _Attributes_ are defined by `HTML`; _properties_ are accessed from `DOM` nodes.
  * A few `HTML` attributes have 1:1 mapping to properties; i.e. `id`
  * Some `HTML` attributes don't have corresponding properties, i.e. `aria-*`
  * Some `DOM` properties don't have corresponding attributes: i.e. `textContent`

  > It is important to remember that `HTML` attributes and the `DOM` property are different things, even when they have the same name.  In `Angular`, the only role of `HTML` attributes is to initialize element and directive state.

**Template binding works with _properties_ and _events_, not _attributes_**.

  > When you write a data-binding, you're dealing exclusively with the `DOM` _properties_ and _events_ of the target.

  > The general rule can help you build a mental model of attributes and `DOM` properties: **Attributes initialize `DOM` properties and then they are done; property values can change; attribute values cannot**.

For more information, see the [MDN Interfaces Documentation](https://developer.mozilla.org/en-US/docs/Web/API#Interfaces) which has API docs for all the standard `DOM` elements and their properties.  Comparing the `<td>` [attributes](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/td) to the `<td>` [properties](https://developer.mozilla.org/en-US/docs/Web/API/HTMLTableCellElement) provides a helpful example for differentiation.  In particular, you can navigate from the attributes page to the properties via "`DOM` interface" link, and navigate the inheritance hierarchy up to `HTMLTableCellElement`.

### Example 1: `<input>`:
When the browser renders `<input type="text" value="Sara">`, it creates a corresponding `DOM` node with a `value` property initialized to "Sarah".

```html
<input type="text" value="Sarah">
```

When the user enters "Sally" into the `<input>`, the `DOM` element `value` _property_ becomes "Sally".  however, if you look at the `HTML` attribute `value` using `input.getAttribute('value')`, you can see that the _attribute_ remains unchanged--it returns "Sarah".

The `HTML` attribute `value` specifies the _initial_ value; the `DOM` `value` property is the _current_ value.

### Example 2: A Disabled `<button>`:
The `disabled` attribute is another example.  A button's `disabled` _property_ is `false` by default, so the button is enabled.

When you add the `disabled` _attribute_, its presence alone initializes the button's `disabled` _property_ to `true` so the button is disabled.

```html
<button disabled>Test Button</button>
```

Adding and removing the `disabled` _attribute_ disables and enables the button.  However, the value of the _attribute_ is irrelevant, which is why you cannot enable a button by writing:

```html
<button disabled="false">Still Disabled</button>
```

To control the state of the button, set the `disabled` _property_.

  > Though you could technically set the `[attr.disabled]` attribute binding, the values are different in that the property binding requires a `boolean` value, while its corresponding attribute binding relies on whether the value is `null` or not.  Consider the following:
  > 
  > ```html
  > <input [disabled]="condition ? true: false">
  > <input [attr.disabled]="condition ? 'disabled' : null">
  > ```

---

[Angular Docs](https://angular.io/guide/template-syntax)