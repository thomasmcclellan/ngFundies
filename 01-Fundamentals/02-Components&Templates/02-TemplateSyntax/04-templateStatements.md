##### 10/07/2019
# Template Syntax - Template Statements
A **template statement** responds to an _event_ raised by a binding target such as an element, component, or directive.  You'll see template statements in the event binding section, appearing in quotes to the right of the `=` symbol as in `(event)="statement"`.

`src/app/app.component.html`:
```html
<button (click)="deleteHero()">Delete Hero</button>
```

A template statement _has a side effect_.  That's the whole point of an event.  It's how you update application state from user action.

  > Responding to events is the other side of `Angular`'s _unidirectional data flow_.  You're free to change anything, anywhere, during this turn of the event loop.

  > Like template expressions, template statements use a language that looks like `JS`.  The template statement parser differs from the template expression parser and specifically supports both basic assignment (`=`) and chaining expressions (with `;` or `,`).

However, certain `JS` syntax is not allowed:
  * `new`
  * Increment/decrement operators (`++` or `--`)
  * Operator assignment (such as `+=` or `-=`)
  * The bitwise operators `|` and `&`
  * The template expression operators

## Statement Context:
As with expressions, statements can refer only to what's in the statement context such as an event handling method of the component instance.

The _statement context_ is typically the component instance.  The `deleteHero` in `(click) = "deleteHero()"` is a method of the data-bound component, as seen above.

The statement context may also refer to properties of the template's own context.  In the following examples, the template `$event` object, a template input variable (`let hero`), and a template reference variable (`#heroForm`) are passed to an event handling method of the component.

`src/app/app.component.html`:
```html
<button (click)="onSave($event)">Save</button>
<button *ngFor="let hero of heroes" (click)="deleteHero(hero)">{{ hero.name }}</button>
<form #heroForm (ngSubmit)="onSubmit(heroForm)"> ... </form>
```

Template context names take precedence over component context names.  In `deleteHero(hero)` above, the `hero` is the template input variable, not the component's `hero` property.

## Statement Guidelines:
Template statements cannot refer to anything in the global namespace.  They can't refer to `window` or `document`.  They can't call `console.log` or `Math.max`.

As with expressions, avoid writing complex template statements.  A method call or simple property assignment should be the norm.

---

[Angular Docs](https://angular.io/guide/template-syntax)