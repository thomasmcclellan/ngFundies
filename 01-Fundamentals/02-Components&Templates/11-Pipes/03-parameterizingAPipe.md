##### 2/24/2020
# Pipes - Parameterizing a Pipe
A pipe can accept any number of optional parameters to fine-tune its output.  To add parameters to a pipe, follow the pipe name with a colon and then the parameter value (such as `currency: 'EUR'`).  If the pipe accepts multiple parameters, separate the values with colons (such as `slice:1:5`).

Modify the birthday template to give the date pipe a format parameter.  After formatting the hero's April 15th birthday, it renders as `04/15/88`:

```hmtl
<p>The hero's birthday is {{ birthday | date:'MM/dd/yy' }}</p>
```

The parameter value van be any valid template expression, such as a `string` literal or a component property.  In other words, you can control the format through a binding the same way you control the birthday value through a binding.

Write a second component that _binds_ the pipe's format parameter to the component's `format` property.  Here's the template for that component:

```ts
template: `
  <p>The hero's birthday is {{ birthday | date:format }}</p>
  <button (click)="toggleFormat()">Toggle Format</button>
`
```

You also added a button to the template and bound its click event to the component's `toggleFormat()` method.  That method toggles the component's `format`between a short form (`'shortDate'`) and a longer form (`'fullDate'`).

```ts
export class HeroBirthday2Component {
  birthday = new Date(1988, 3, 15); // April 15, 1988
  toggle: boolean = true; // starts with true === shortDate

  get format() { return this.toggle ? 'shortDate' : 'fullDate'; }
  toggleFormat() { this.toggle = !this.toggle; }
}
```

As you click the button, the displayed date alternates between `'04/15/1988'` and `'Friday, April 15, 1988'`.

![Date Pipe](../../../Assets/datePipe.gif)

  > Read more about the `DatePipe` format option in the [Date Pipe](https://angular.io/api/common/DatePipe) API Reference page.

---

[Angular Docs](https://angular.io/guide/pipes#parameterizing-a-pipe)