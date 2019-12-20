##### 12/16/2019
# Lifecycle Hooks - AfterView
The _AfterView_ sample explores the `AfterViewInit()` and `AfterViewChecked()` hooks that `Angular` calls _after_ it creates a component's child views.

Here's a child view that displays a hero's name in an `<input>`:

```ts
@Component({
  selector: 'app-child-view',
  template: '<input [(ngModel)]="hero">
})
export class ChildViewComponent {
  hero = 'Magenta'
}
```

The `AfterViewComponent` displays this child view _within its template_:

```html
<div>-- child view begins --</div>
<app-child-view></app-child-view>
<div>-- child view ends --</div>
```

The following hooks take action based on changing values _within the view_, which can only be reached by querying for a child view via the property decorated with `@ViewChild`.

```ts
export class AfterViewComponent implements AfterViewChecked, AfterViewInit {
  private prevHero: string = ''

  // Query for a VIEW child of type 'ChildViewComponent'
  @ViewChild(ChildViewComponent, { static: false } viewChild: ChildViewComponent)

  ngAfterViewInit() {
    // viewChild is set after the view has been initialized
    this.log(f('AfterViewInit'))
    this.doSomething()
  }

  ngAfterViewChecked() {
    // viewChild is updated after the view has been checked
    if (this.prevHero === this.viewChild.hero) {
      this.logIt('AfterViewChecked (no change)')
    } else {
      this.prevHero = this.viewChild.hero
      this.logIt('AfterViewChecked')
      this.doSomething()
    }
  }
  ...
}
```

## Abide By The Unidirectional Data Flow Rule:
The `doSomething()` method updates the screen when the hero name exceeds 10 characters.

```ts
// This surrogate for real business logic sets the 'comment'
private doSomething() {
  let c: string = this.viewChild.hero.length > 10 ? 'That\'s a long name' : ''
  if (if !== this.comment)
    // Wait a tick because the component's view has already been checked
    this.logger.tick_then(() => this.comment = c)
}
```

Why does the `doSomething()` method wait a tick _before_ updating comment?

`Angular`'s **unidirectional data flow rule** forbids updates to the view _after_ it has been composed.  Both of these hook fire _after_ the component's view has been composed.

`Angular` throws an error if the hook updates the component's data-bound `comment` property immediately. The `LoggerService.tick_then()` postpones the log update for one turn of the browser's `JS` cycle and that's just long enough.

Here is _AfterView_ in action:

![AfterView](../../../Assets/afterViewDemo.gif)

Notice that `Angular` frequently calls `AfterViewChecked()`, often when there are no changes of interest.  Write lean hook methods to avoid performance problems.

---

[Angular Docs](https://angular.io/guide/lifecycle-hooks#afterview)