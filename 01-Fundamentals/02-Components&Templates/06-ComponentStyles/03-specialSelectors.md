##### 1/03/2020
# Component Styles - Special Selectors
Component styles have a few special _selectors_ from the world of shadow `DOM` style scoping (described in the [`CSS` Scoping Module Level 1](https://www.w3.org/TR/css-scoping-1/) page on the W3C site).  The following sections describe these selectors.

## `:host`:
Use the `:host` pseudo-class selector to target styles in the element that _hosts_ the component (as opposed to targeting elements _inside_ the component's template).

```css
:host {
  display: block;
  border: 1px solid black
}
```

The `:host` selector is the only way to target the host element.  YOu can't reach the host element from inside the component with other selectors because it's not part of the component's own template.  The host element is in a parent component's template.

Use the _`function` form_ to apply host styles conditionally by including another selector inside parentheses after `:host`.

The next example targets the host element again, but only when it also has the `active` `CSS` class.

```css
:host(.active) {
  border-width: 3px;
}
```

## `:host-context`:
Sometimes it's useful to apply styles based on some condition _outside_ of a component's view.  For example, a `CSS` theme class could be applied to the document `<body>` element, and you want to change how your component looks based on that.

Use the `:host-context()` pseudo-class selector, which works just like the `function` form of `:host()`.  The `:host-context()` selector looks for a `CSS` class in any ancestor of the component host element, up to the document root.  The `:host-context()` selector is useful when combined with another selector.

The following example applies a `background-color` style to all `<h2>` elements _inside_ the component, only if some ancestor element has the `CSS` class `theme-light`.

```css
:host-context(.theme-light) h2 {
  background-color: #eef;
}
```

## (<span style="color: red">Deprecated</span>) `/deep/`, `>>>`, and `::ng-deep`:
Component styles normally apply only to the `HTML` in the component's own template.

Applying the `::ng-deep` pseudo-class to any `CSS` rule completely disables view-encapsulation for that rule.  Any style with `::ng-deep` applied becomes a global style.  In order to scope the specified style to the current component and all its descendants, be sure to include the `:host` selector before `::ng-deep`. If the `::ng-deep` combinator is used without the `:host` pseudo-class selector, the style can bleed into other components.

The following example targets all `<h3>` elements, from the host element, down through this component to all of its child elements in the `DOM`.

```css
:host /deep/ h3 {
  font-style: italic;
}
```

The `/deep/` combinator also has the aliases `>>>` and `::ng-deep`.

  > Use `/deep/`, `>>>`, and `::ng-deep` only with _emulated_ view encapsulation.  Emulated is the default and most commonly used view encapsulation.  For more information, see the Controlling View Encapsulation section.

  > The shadow-piercing descendant combinator is deprecated and [support is being removed from major browsers](https://www.chromestatus.com/features/6750456638341120) and tools.  As such, we plan to drop support in `Angular` (for all three: `/deep/`, `>>>`, and `::ng-deep`).  Until then, `::ng-deep` should be preferred for a broader compatibility with the tools.

---

[Angular Docs](https://angular.io/guide/component-styles#special-selectors)