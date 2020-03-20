##### 2/24/2020
# Pipes - Overview
Every application starts out with what seems like a simple task: get data, transform them, and show them to users.  Getting data could be as simple as creating a local variable or as complex as streaming data over a WebSocket.

Once data arrives, you could push their raw `toString` values directly to the view, but rately makes for a good user experience.  For example, in most use cases, users prefer to see a date in a simple format like `April 15, 1988` rather than the raw `string` format `Fir Apr 15 1988 00:00:00 GMT-0700 (Pacific Daylight Time)`.

Clearly, some values benefit from a bit of editing.  YOu may notic that you desire many of the same transformations repeatedly, both within and across many applications.  You can almost think of them as styles.  In fact, you might like to apply them in your `HTML` templates as you do styles.

Introducing `Angular` pipes, a way to write display-value transformations that you can declare in your `HTML`.

## Using Pipes:
A pipe takes in data as input as transforms it to a desired output.  In this page, you'll use pipes to transform a component's birthday property into a human-friendly date.

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-hero-birthday',
  template: `<p>The hero's birthday is {{ birthday | date }}</p>`
})
export class HeroBirthdayComponent {
  birthday = new Date(1988, 3, 15); // April 15, 1988
}
```

Focus on the component's template.

```html
<p>The hero's birthday is {{ birthday | date }}</p>
```

Inside the interpolation expression, you flow the component's `birthday` value through the [pipe operator](https://angular.io/guide/template-syntax#pipe) (`|`) to the [Date pipe](https://angular.io/api/common/DatePipe) `function` on the right.  All pipes work this way.

---

[Angular Docs](https://angular.io/guide/pipes)