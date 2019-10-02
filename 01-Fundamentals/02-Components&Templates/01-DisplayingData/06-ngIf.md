##### 9/30/2019
# Introduction to Displaying Data - Conditional Display with `*ngIf`
Sometimes an app needs to display a view or a portion of a view only under specific circumstances.

Let's change the example to display a message if there are more than three heroes.

The `Angular` `*ngIf` directive inserts or removes an element based on a _truthy/falsy_ condition.  To see it in action, add the following paragraph at the bottom of the template.

`src/app/app.component.ts` (message):
```html
<p *ngIf="heroes.length > 3">There are many heroes!</p>
```

  > Don't forget the leading asterisk (*) in `*ngIf`.  It is an essential part of the syntax.

The template expression inside the double quotes, `*ngIf="heroes.length > 3"`, looks and behaves much like `TS`.  When the component's list of heroes has more than three items, `Angular` adds the paragraph to the `DOM` and the message appears.  If there are three or fewer items, `Angular` omits the paragraph, so no message appears.  

  > `Angular` isn't showing or hiding the message. It is adding and removing the paragraph element from the `DOM`.  That improves performance, especially in large projects when conditionally including or excluding big chucks of `HTML` with many data bindings.

---

[Angular Docs](https://angular.io/guide/displaying-data)