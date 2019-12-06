##### 12/02/2019
# User Input - Binding to User Input Events
You can use `Angular` event binding to respond to any `DOM` event.  Many `DOM` events are triggered by user input.  Binding to these events provides a way to get input from the user.

To bind to a `DOM` event, surround the `DOM` event name in parentheses and assign a quoted template statement to it.

The following example shows an event binding that implements a click handler:

```html
<button (click)="onClickMe()">Click me!</button>
```

When writing a binding, be aware of a template statement's _execution content_.  the identifiers in a template statement belongs to a specific context `object`, usually the `Angular` component controlling the template.  the example above shows a single line of `HTML`, but that `HTML` belongs to a larger component:

```ts
@Component({
  selector: 'app-click-me',
  template: `
    <button (click)="onClickMe()">Click me!</button>
    {{ clickMessage }}
  `
})
export class ClickMeComponent {
  clickMessage: string = ''

  onClickMe() : void {
    this.clickMessage = 'You are my hero!'
  }
}
```

When the user clicks the button, `Angular` calls the `onClickMe` method from the `ClickMeComponent`.

---

[Angular Docs](https://angular.io/guide/user-input)