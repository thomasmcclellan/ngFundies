##### 1/09/2020
# `Angular` Elements - Overview
_`Angular` elements_ are `Angular` components packaged as _custom elements_ (also called **Web Components**), a web standard for defining new `HTML` elements in a framework-agnostic way.

[Custom elements](https://developer.mozilla.org/en-US/docs/Web/Web_Components/Using_custom_elements) are Web Platform feature currently supported by Chrome, Firefox, Opera, and Safari, and available in other browsers through polyfills.  A custom element extends `HTML` by allowing you to define a tag whose content is created and controlled by `JS` code.  The browser maintains a `CustomElementRegistry` of defined custom elements, which maps an instantiable `JS` class to an `HTML` tag.

The `@angular/elements` package exports a `createCustomElement()` API that provides a bridge from `Angular`'s components interface and change detection functionality to the built-in `DOM` API.

Transforming a component to a custom element makes all of the required `Angular` infrastructure available to the browser.  Creating a custom element is simple and straightforward,a nd automatically connects your component-defined view with change detection view with change detection and data binding, mapping `Angular` functionality to the corresponding native `HTML` equivalents.

  > We are working on custom elements that can be used by web apps built on other frameworks.  A minimal, self-contained version of the `Angular` framework will be injected as a service to support the component's change-detection and data-binding functionality.  For more about the direction of development, check out this [video presentation](https://www.youtube.com/watch?v=Z1gLFPLVJjY&t=4s).


---

[Angular Docs](https://angular.io/guide/elements)