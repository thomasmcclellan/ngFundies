##### 1/02/2020
# Component Styles - Style Scope
  > **NOTE**: The styles specified in `@Component` metadata _apply only within the template of that component_.

They are _not inherited_ by any components nested within the template, nor by any content projected into the component.

In this example, the `h1` style applies only to the `HeroAppComponent`, not the nested `HeroMainComponent` nor to `<h1>` tags anywhere else in the application.

This scoping restriction is a **_styling modularity feature_**.
  * You can use the `CSS` class names and selectors that make the most sense in the context of each component
  * Class names and selectors are local to the component and don't collide with classes and selectors used elsewhere in the application
  * Changes to styles elsewhere in the application don't affect the component's styles
  * You can co-locate the `CSS` code of each component with the `TS` and `HTML` code of the component, which leads to a neat and tidy project structure.
  * You can change or remove component `CSS` code without searching through the whole application to find where else the code is used

---

[Angular Docs](https://angular.io/guide/component-styles#style-scope)