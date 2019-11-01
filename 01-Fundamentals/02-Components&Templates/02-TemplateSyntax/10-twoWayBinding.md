##### 10/23/2019
# Template Syntax - Two-Way Binding `[(...)]`
**Two-way binding** gives your app a way to share data between a component class and its template.

## Basics of Two-Way Binding:
Two-way binding does two things:
  1. Sets a specific element property
  2. Listens for an element change event

`Angular` offers a special _two-way data binding_ syntax for this purpose, `[()]`.  The `[()]` syntax combines the brackets of property binding (`[]`) with the parentheses of event binding (`()`).

  > **Banana in a box:**
  >
  > Visualize a _banana in a box_ to remember that the parentheses go _inside_ the brackets.

The `[()]` syntax is easy to demonstrate when the element has a settable property called `x` and a corresponding event named `xChange`.  Here's a `SizerComponent` that fits this pattern.  It has a `size` value property and a companion `sizeChange` event:

`sizer.component.ts`:
```typescript
import { Component, Input, Output, EventEmitter } from '@angular/core';

@Component({
  selector: 'app-sizer',
  templateUrl: './sizer.component.html',
  styleUrls: ['./sizer.component.css']
})
export class SizerComponent {
  @Input() size: number | string
  @Input() sizeChange = new EventEmitter<number>()

  dec() { this.resize(-1) }
  inc() { this.resize(+1) }

  resize(delta: number) {
    this.size = Math.min(40, Math.max(8, +this.size + delta))
    this.sizeChange.emit(this.size)
  }
}
```

The initial `size` is an input value from a property binding.  Clicking the buttons increases or decreases the `size`, within min/max value constraints, and then raises, or emits, the `sizeChange` event with the adjusted size.

Here's an example in which the `AppComponent.fontSizePx` is two-way bound to the `SizerComponent`:

`app.component.html` (two-way-1):
```html
<app-sizer [(size)]="fontSizePx"></app-sizer>
<div [style.font-size.px]="fontSizePx">Resizable Text</div>
```

The `AppComponent.fontSizePx` establishes the initial `SizerComponent.size` value.

`app.component.ts`:
```typescript
fontSizePx = 16
```

Clicking the buttons updates the `AppComponent.fontSizePx` via two-way binding.  The revised `AppComponent.fontSizePx` value flows through to the _style_ binding, making the displayed text bigger or smaller.

The two-way binding syntax is really just syntatic sugar for a _property_ binding and an _event_ binding.  `Angular` desugars the `SizerComponent` binding into this:

`app.component.html` (two-way-2):
```html
<app-sizer [size]="fontSizePx" (sizeChange)="fontSizePx=$event"></app-size>
```

The `$event` variable contains the payload of the `SizerComponent.sizeChange` event.  `Angular` assigns the `$event` value to the `AppComponent.fontSizePx` when the user clicks the buttons.

## Two-Way Binding in Forms:
The two-way binding syntax is a great convenience compared to separate property and event binding.  It would be convenient to use two-way binding with `HTML` form elements like `<input>` and `<select>`.  However, no native `HTML` element follows the `x` value and `xChange` event pattern.

---

[Angular Docs](https://angular.io/guide/template-syntax#two-way-binding-)