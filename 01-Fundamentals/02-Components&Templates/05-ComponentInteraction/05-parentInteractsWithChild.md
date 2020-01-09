##### 12/27/2019
# Component Interaction - Parent Interacts With Child Via _Local Variable_
A parent component cannot use data binding to read child properties or invoke child methods.  You can do both by creating a template reference variable for the child element and then reference that variable _within the parent template_ as seen in the following example.

The following is a child `CountdownTimerComponent` that repeatedly counts down to zero and launches a rocket.  It has `start` and `stop` methods that control the clock and it displays a countdown status message in its own template.

```ts
import { Component, OnDestroy, OnInit } from '@angular/core';

@Component({
  selector: 'app-countdown-timer',
  template: '<p>{{ message }}</p>'
})
export class CountdownTimerComponent implements OnInit, OnDestroy {
  intervalId: number = 0
  message: string = ''
  seconds: number = 11

  ngOnInit() {
    this.start()
  }

  ngOnDestroy() {
    this.clearTimer()
  }

  clearTimer() : void {
    clearInterval(this.intervalId)
  }

  start() : void {
    this.countDown()
  }

  stop() : void {
    this.clearTimer()
    this.message = `Holding a T-${this.seconds} seconds`
  }

  private countDown() : void {
    this.clearTimer()
    this.intervalId = window.setInterval(() => {
      this.seconds -= 1

      if (this.seconds === 0) {
        this.message = 'Blast off!'
      } else {
        if (this.seconds < 0)
          this.seconds = 10 // reset

        this.message = `T-${this.seconds} seconds and counting`
      }
    }, 1000) 
  }
}
```

The `CountdownLocalVarParentComponent` that hosts the timer component is as follows:

```ts
import { Component } from '@angular/core';
import { CountdownTimerComponent } from './countdown-timer.component';

@Component({
  selector: 'app-countdown-parent-lv',
  template: `
    <h3>Countdown to Liftoff (via local variable)</h3>
    <button (click)="timer.start()">Start</button>
    <button (click)="timer.stop()">Stop</button>
    <div class="seconds">{{ timer.seconds }}</div>
    <app-countdown-timer #timer></app-countdown-timer>  
  `,
  styleUrls: ['../assets/demo.css']
 })
 export class CountdownLocalVarParentComponent { }
```

The parent component cannot data bind to the child's `start` and `stop` methods nor to its `seconds` property.

You can place a local variable, `#timer`, on the tag `<countdown-timer>` representing the child component.  That gives you a reference to the child component and the ability to access _any of its properties or methods_ from within the parent template.

This example wires parent buttons to the child's `start` and `stop` and uses interpolation to display the child's `seconds` property.

Here, we see the parent and child working together:

![Parent/Child With Local Variable](../../../Assets/localVariableDemo.gif)

## Test It:
Tes that the seconds displayed in the parent template match the seconds displayed in the child's status message.  Test also that clicking the _stop_ button pauses the countdown timer:

```ts
//...
it('timer and parent seconds should match', () => {
  const parent = element(by.tagName(parentTag))
  const message = parent.element(by.tagName('app-countdown-timer')).getText()
  const seconds = parent.element(by.className('seconds')getText())
  browser.sleep(10) // give 'seconds' a change to catchup with 'message'

  expect(message).toContain(seconds)
})

it('should stop the countdown', () => {
  const parent = element(by.tagName(parentTag))
  const stopButton = parent.all(by.tagName('button')).get(1)

  stopButton.click()
    .then(() => {
      const message = parent.element(by.tagName('app-countdown-timer')).getText()

      expect(message).toContain('Holding')
    })
})
//...
```

---

[Angular Docs](https://angular.io/guide/component-interaction#parent-interacts-with-child-via-local-variable)