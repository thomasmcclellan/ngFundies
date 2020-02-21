##### 1/20/2020
# `Angular` Elements - Typings For Custom Elements
Generic `DOM` APIs, such as `document.createElement()` or `document.querySelector()`, return an element type that is appropriate for the specified arguments.  For example, calling `document.createElement('a')` will return an `HTMLAnchorElement`, which `TS` knows has a `href` property.  Similarly, `document.createElement('div')` will return an `HTMLDivElement`, which `TS` knows has no `href` property.

When called with unknown elements, such as a custom element name (`popup-element` in our example), the methods will return a generic type, such as `HTMLElement`, since `TS` can't infer the correct type of the returned element.

Custom elements created with `Angular` extend `NgElement` (which in turn extends `HTMLElement`).  Additionally, these custom elements will have a property for each input of the corresponding component.  For example, our `popup-element` will have a `message` property of type `string`.

There are a few options if you want to get correct types of your custom elements.  Let's assume you create a `my-dialog` custom element based on the following component:

```ts
@Component(...)
class MyDialog {
  @Input() content: string
}
```

The most straight forward way to get accurate typings is to cast the return value of the relevant `DOM` methods to the correct type.  For that, you can use the `NgElement` and `WithProperties` types (both exported from `@angular/elements`):

```ts
const aDialog = document.createElement('my-dialog') as NgElement & WithProperties<{ content: string }>
aDialog.content = 'Hello, world'
aDialog.content = 123 // ERROR => TS is looking for a string
aDialog.content = 'News' // ERROR => TS knows there is no 'body' property on 'aDialog'
```

This is a good way to quickly get `TS` features, such as type checking and autocomplete support, for your custom element.  But it can get cumbersome if you need it in several places, because you have to cast the return type on every occurrence.

An alternative way, that only requires defining each custom element's type once, is augmenting the `HTMLElementTagNameMap`, which `TS` uses to infer the type of a returned element based on its tag name (for `DOM` methods such as `document.createElement()`, `document.querySelector()`, etc.):

```ts
declare global {
  interface HTMLElementTagNameMap {
    'my-dialog': NgElement & WithProperties<{ content: string }>
    'my-other-element': NgElement & WithProperties<{ foo: 'bar' }>
    ...
  }
}
```

Now, `TS` can infer the correct type the same way it does for built-in elements:

```ts
document.createElement('div') // HTMLDivElement (built-in element)
document.querySelector('foo') // Element (unknown element)
document.createElement('my-dialog') // NgElement & WithProperties<{ content: string }> (custom element)
document.querySelector('my-other-element') // NgElement & WithProperties<{ foo: 'bar' }> (custom element)
```

---

[Angular Docs](https://angular.io/guide/elements#typings-for-custom-elements)