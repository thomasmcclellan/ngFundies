##### 2/03/2020
# Attribute Directives - Apply The Attribute Directive
To use the new `HighlightDirective`, add a paragraph (`<p>`) element to the template of the root `AppComponent` and apply the directive as an attribute.

```html
<p appHighlight>Highlight me!</p>
```

Now run the application to see the `HighlightDirective` in action 

```
ng serve
```

To summarize, `Angular` found the `appHighlight` attribute on the **host** `<p>` element.  It created an instance of the `HighlightDirective` class and injected a reference to the `<p>` element into the directive's constructor which sets the `<p>` element's background style to yellow.

---

[Angular Docs](https://angular.io/guide/attribute-directives#apply-the-attribute-directive)