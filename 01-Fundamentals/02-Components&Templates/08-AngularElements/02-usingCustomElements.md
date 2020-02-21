##### 1/10/2020
# `Angular` Elements - Using Custom Elements
Custom elements bootstrap themselves--they start automatically when they are added to the `DOM`, and are automatically destroyed when removed from the `DOM`.  Once a custom element is added to the `DOM` for any page, it looks and behaves like any other `HTML` element, and does not require any special knowledge of `Angular` terms or usage conventions.
  * **Easy dynamic content in an `Angular` app**:  transforming a component to a custom element provides an easy path to creating dynamic `HTML` content in your `Angular` app.  `HTML` content that you add directly to the `DOM` in an `Angular` app is normally displayed without `Angular` processing, unless you define a _dynamic component_, adding your own code to connect the `HTML` tag to your app data, and participate in change detection.  With a custom element, all of that wiring is taken care of automatically.
  * **Content-rich applications**: if you have a content-rich app, such as the `Angular` app that presents this documentation, custom elements let you give your content providers sophisticated `Angular` functionality without requiring knowledge of `Angular`.  For example, an `Angular` guide like this one is added directly to the `DOM` by the `Angular` navigation tools, but can include special elements like `<code-snippet>` that perform complex operations.  All you need to tell you content provider is the syntax of your custom element.  They don't need to know anything about `Angular`, or anything about your component's data structure or implementation.

## How It Works:
Use the `createCustomElement()` function to convert a component into a `class` that can be registered with the browser as a custom element.  After you register your configured `class` with the browser's custom-element registry, you can use the new element just like a built-in `HTML` element in content ath you add directly into the `DOM`:

```html
<my-popup message="Use Angular!"></my-popup>
```

When your custom element is placed on a page, the browser creates an instance of the registered class and adds it to the `DOM`.  The content is provided by the component's template, which uses `Angular` template syntax, and is rendered using the component and `DOM` data.  Input properties in the component correspond to input attributes for the element.

![Custom Element](../../../Assets/customElement.png)

---

[Angular Docs](https://angular.io/guide/elements#using-custom-elements)