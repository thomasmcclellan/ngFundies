##### 11/08/2019
# Template Syntax - `@Input()` and `@Output()` Properties
`@Input()` and `@Output()` allow `Angular` to share data between the parent context and child directives or components.  An `@Input()` property is writable while an `@Output()` property is observable.

Consider this example of a child/parent relationship:

```html
<parent-component>
  <child-component></child-component>
</parent-component>
```

Here, the `<child-component>` selector, or child directive, is embedded within a `<parent-component>`, which serves as the child's context.

`@Input()` and `@Output()` act as the API, or application programming interface, of the child component in that they allow the child to communicate with the parent.  Think of `@Input()` and `@Output()` like ports or doorways--`@Input()` is the doorway into the component allowing data to flow in while `@Output()` is the doorway out of the component, allowing the child component to send data out.

  > `@Input()` and `@Output()` **are independent**!
  >
  > Though `@Input()` and `@Output()` often appear together in apps, you can use them separately.  If the nested component is such that it only needs to send data to its parent, you wouldn't need an `@Input()`, only an `@Output()`.  The reverse is also true in that if the child only needs to receive data from the parent, you'd only need `@Input()`.
---

[Angular Docs](https://angular.io/guide/template-syntax#input-and-output-properties)