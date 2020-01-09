##### 12/30/2019
# Component Interaction - Parent Call An `@ViewChild()`
The _local variable_ approach is simple and easy.  But it is limited because the parent-child wiring must be done entirely within the parent template.  The parent component _itself_ has no access to the child.

You can't use the _local variable_ technique if an instance of the parent component _class_ must read or write child component values or must call child component methods.

When the parent component _class_ requires that kind of access, **_inject_** the child component into the parent as a _ViewChild_.

  > **NOTE**: The following example illustrates this technique with the same Countdown Timer example.  Neither its appearance nor its behavior will change.  The child `CountdownTimerComponent` is the same as well.

Here is the parent, `CountdownViewChildParentComponent`:

```ts
import { AfterViewInit, ViewChild, Component } from '@angular/core';
import { CountdownTimerComponent } from './countdown-timer.component';

@Component({
  selector: 'app-countdown-parent-vc',
  template: `
    <h3>Countdown to Liftoff (via ViewChild)</h3>
    <button (click)="start()">Start</button>
    <button (click)="stop()">Stop</button>
    <div class="seconds">{{ seconds() }}</div>
    <app-countdown-timer></app-countdown-timer>
  `,
  styleUrls: ['../assets/demo.css']
})
export class CountdownViewChildParentComponent implements AfterViewInit {
  @ViewChild(CountdownTimerComponent, { static: false })

  private timerComponent: CountdownTimerComponent

  seconds() : number { return 0 }

  ngAfterViewInit() {
    // Redefine 'seconds()' to get from the 'CountdownTimerComponent.seconds'
    // but wait a tick first to avoid one-time devMode
    // unidirectional-data-flow-violation error
    setTimeout(() => this.timerComponent.seconds, 0)
  }

  start() : void { this.timerComponent.start() }
  stop() : void { this.timerComponent.stop() }
} 
```

It takes a bit more work to get the child view into the parent component _class_.

First, you have to import reference to the `ViewChild` decorator and the `AfterViewChildInit` lifecycle hook.

Next, inject the child `CountdownTimerComponent` into the private `timerComponent` property via the `@ViewChild()` property decorator.

The `#timer` local variable is gone from the component metadata.  Instead, bind the buttons to the parent component's own `start` and `stop` methods and present the ticking seconds in an interpolation around the parent component's `seconds` method.

These methods access the injected timer component directly.

The `ngAfterViewInit()` lifecycle hook is an important wrinkle.  The timer component isn't available until _after_ `Angular` displays the parent view.  So it displays 0 seconds initially.

Then `Angular` calls the `ngAfterViewInit()` lifecycle hook at which time it is _too_ late to update the parent view's display of the countdown seconds.  `Angular`'s unidirectional data flow rule prevents updating the parent view's in the same cycle.  The app has to _wait one turn_ before it can display the seconds.

Use `setTimeout()` to wait one tick and then revise the `seconds()` method so that it takes future values from the timer component.

---

[Angular Docs](https://angular.io/guide/component-interaction#parent-calls-an-viewchild)