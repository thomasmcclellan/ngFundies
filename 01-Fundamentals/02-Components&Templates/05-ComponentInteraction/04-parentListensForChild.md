##### 12/26/2019
# Component Interaction - Parent Listens For Child Event
The child component exposes an `EventEmitter` property with which it `emits` events when something happens.  The parent binds to the event property and reacts to those events.

The child's `EventEmitter` property is an **_output property_**, typically adorned with an @Output decoration as seen in this `VoterComponent`:

```ts
import { Component, EventEmitter, Input, Output } from '@angular/core';

@Component({
  selector: 'app-voter',
  template: `
    <h4>{{ name }}</h4>
    <button 
      (click)="vote(true)"
      [disabled]="didVote"
    >
      Agree
    </button>
    <button 
      (click)="vote(false)"
      [disabled]="didVote"
    >
      Agree
    </button>
  `
})
export class VoterComponent {
  @Input() name: string
  @Output() voted = new EventEmitter<boolean>()

  didVote = false

  vote(agreed: boolean) : void {
    this.voted.emit(agreed)
    this.didVote = true
  }
}
```

Clicking a button triggers emission of a `true` or `false`, the boolean _payload_.

The parent `VoteTakerComponent` binds an event handler called `onVoted()` that responds to the child event payload `$event` and updates a counter.

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-vote-taker',
  template: `
    <h2>Should mankind colonize the universe?</h2>
    <h3>Agree: {{ agreed }}, Disagree: {{ disagreed }}</h3>
    <app-voter 
      *ngFor="let voter of voters"
      [name]="voter"
      (voted)="onVoted($event)"
    ></app-voter>
  `
})
export class VoteTakerComponent {
  agreed = 0
  disagreed = 0
  voters = ['Tim', 'Jim', 'Kim']

  onVoted(agreed: boolean) : void {
    agreed ? this.agreed++ : this.disagreed++
  }
}
```

The framework passes the event argument--represented by `$event`--to the handler method, and the method processes it:

![Event Handler](../../../Assets/eventHandlerDemo.gif)

## Test It:
Test that clicking the _Agree_ and _Disagree_ buttons update the appropriate counters:

```ts
//...
it('should not emit the event initially', () => {
  const voteLabel = element(by.tagName('app-vote-taker'))
    .element(by.tagName('h3')).getText()

  expect(voteLabel).toBe('Agree: 0, Disagree: 0')
})

it('should process Agree vote', () => {
  const agreeButton1 = element.all(by.tagName('app-voter')).get(0)
    .all(by.tagName('button')).get(0)
  agreeButton1.click()
    .then(() => {
      const voteLabel = element(by.tagName('app-vote-taker'))
        .element(by.tagName('h3')).getText()

      expect(voteLabel).toBe('Agree: 1, Disagree: 0')
    })
})

it('should process Disagree vote', () => {
  const agreeButton1 = element.all(by.tagName('app-voter')).get(1)
    .all(by.tagName('button')).get(1)
  agreeButton1.click()
    .then(() => {
      const voteLabel = element(by.tagName('app-vote-taker'))
        .element(by.tagName('h3')).getText()

      expect(voteLabel).toBe('Agree: 1, Disagree: 1')
    })
})
//...
```

---

[Angular Docs](https://angular.io/guide/component-interaction#parent-listens-for-child-event)