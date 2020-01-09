##### 1/08/2020
# Component Styles - Inspecting Generated `CSS`
When using emulated view encapsulation, `Angular` preprocesses all component styles so that they approximate the standard shadow `CSS` scoping rules.

In the `DOM` of a running `Angular` application with emulated view encapsulation enabled, each `DOM` element has some extra attributes attached to it:

```html
<hero-details _nghost-pmm-5>
  <h2 _ngcontent-pmm-5>Mister Fantastic</h2>
  <hero-team _ngcontent-pmm-5 _nghost-pmm-6>
    <h3 _ngcontent-pmm-6>Team</h3>
  </hero-team>
</hero-details>
```

There are two kinds of generated attributes:
  * An element that would be a shadow `DOM` host in native encapsulation has a generated `_nghost` attribute.  this is typically the case for component host elements
  * An element within a component's view has a `_ngcontent` attribute that identifies to which host's emulated shadow `DOM` this element belongs

The exact values of these attributes aren't important.  They are automatically generated and you never refer to them in application mode.  but they are targeted by the generated component styles, which are in the `<head>` section of the `DOM`:

```css
[_nghost-pmm-5] {
  display: block;
  border: 1px solid black;
}

h3[_ngcontent-pmm-6] {
  background-color: white;
  border: 1px solid black;
}
```

These styles are post-processed so that each selector is augmented with `_nghost` or `_ngcontent` attribute selectors.  These extra selectors enable the scoping rules described in this page.

---

[Angular Docs](https://angular.io/guide/component-styles#loading-component-styles)