##### 1/16/2020
# `Angular` Elements - Browser Support For Custom Elements
The recently-developed [custom elements](https://developer.mozilla.org/en-US/docs/Web/Web_Components/Using_custom_elements) Web Platform feature is currently supported natively in a number of browsers.  Support is pending or planned in other browsers.

| Browser | Custom Element Support |
|---|---|
| Chrome | Supported natively |
| Opera | Supported natively |
| Safari | Supported natively |
| Firefox | Supported natively as of **version 63**.  In older versions: Set the `dom.webcomponents.enabled` and `dom.webcomponents.customelements.enabled` preferences to `true` |
| Edge | Working on an implementation |

In browsers that support Custom Elements natively, the specification requires developers use `ES2015` classes to define Custom Elements--developers can opt-in to this by setting the `target: 'es2015'` property in their project's `tsconfig.json`.  As Custom Element and `ES2015` support may not be available in all browsers, developers can instead choose to use a polyfill to support older browsers and `ES5` code.

Use the `Angular` CLI to automatically set up your project with the correct polyfill: `ng add @angular/elements --name=*your_project_name*`.

---

[Angular Docs](https://angular.io/guide/elements#browser-support-for-custom-elements)