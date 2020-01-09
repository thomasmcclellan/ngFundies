##### 12/30/2019
# Component Interaction - Parent And Children Communicate Via a Service
A parent component and its children share a service whose interface enables bi-directional communication _within the family_.

The scope of the service instance is the parent component and its children.  Components outside this component subtree have no access to the service or their communications.

This `MissionService` connects the `MissionControlComponent` to multiply `AstronautComponent` children.

```ts
import { Injectable } from '@angular/core';
import { Subject } from 'rxjs';

@Injectable()
export class MissionService {
  // Observable string sources
  private missionAnnouncedSource = new Subject<string>()
  private missionConfirmedSource = new Subject<string>()

  // Observable string streams
  missionAnnounced$ = this.missionAnnouncedSource.asObservable()
  missionConfirmed$ = this.missionConfirmedSource.asObservable()

  // Service message commands
  announceMission(mission: string) : void {
    this.missionAnnouncedSource.next(mission)
  }
  confirmMission(astronaut: string) : void {
    this.missionConfirmedSource.next(mission)
  }
}
```

The `MissionControlComponent` both provides the instance of the service that it shares with its children (through the `providers` metadata `array`) and injects that instance into itself through its constructor:

```ts
import { Component } from '@angular/core';
import { MissionService } from './mission.service';

@Component({
  selector: 'app-mission-control',
  template: `
    <h2>Mission Control</h2>
    <button (click)="announce()">Announce Mission</button>
    <app-astronaut
      *ngFor="let astronaut of astronauts"
      [astronaut]="astronaut"
    ></app-astronaut>
    <h3>History</h3>
    <ul>
      <li *ngFor="let event of history">{{ event }}</li>
    </ul>
  `,
  providers: [MissionService]
})
export class MissionControlComponent {
  astronauts: string[] = ['Lovell', 'Swigert', 'Haise']
  history: string[] = []
  missions: string[] = [
    'Fly to the moon!',
    'Fly to Mars!',
    'Fly to Titan!'
  ]
  nextMission: number = 0

  constructor(private missionService: MissionService) {
    missionService.missionConfirmed$.subscribe(astronaut => {
      this.history.push(`${astronaut} confirmed for mission`)
    })
  }

  announce() : void {
    const mission = this.missions[this.nextMission++]
    this.missionService.announceMission(mission)
    this.history.push(`Mission ${mission} announced`)

    if (this.nextMission >= this.mission.length)
      this.nextMission = 0
  }
}
```

The `AstronautComponent` also injects the service in its constructor.  Each `AstronautComponent` is a child of the `MissionControlComponent` and therefore receives its parent's service instance:

```ts
import { Component, Input, OnDestroy } from '@angular/core';
import { MissionService } from './mission.service';
import { Subscription } from 'rxjs';

@Component({
  selector: 'app-astronaut',
  template: `
    <p>
      {{ astronaut }}: <b>{{ mission }}</b>
      <button
        (click)="confirm()"
        [disabled]="!announced || confirmed"
      >
        Confirm
      </button>
    </p>
  `
})
export class AstronautComponent implements OnDestroy {
  @Input() astronaut: string
  mission: string = '<no mission announced>'
  confirmed: boolean = false
  announced: boolean = false
  subscription = Subscription

  constructor(private missionService: MissionService) {
    this.subscription = missionService.missionAnnounced$.subscribe(mission => {
      this.mission = mission
      this.announced = true
      this.confirmed = true
    })
  }

  confirm() : void {
    this.confirmed = true
    this.missionService.confirmMission(this.astronaut)
  }

  ngOnDestroy() {
    // Prevent memory leak when component destroyed
    this.subscription.unsubscribe()
  }
}
```

  > **NOTE**: This example captures the `subscription` and `unsubscribe()` when the `AstronautComponent` is destroyed.  This is a memory-leak guard step.  There is no actual risk in this app because the lifetime of a `AstronautComponent` is the same as the lifetime of the app itself.  That _would not_ always be true in a more complex application.
  >
  > You don't add this guard to the `MissionControlComponent` because, as the parent, it controls the lifetime of the `MissionService`.

The _History_ log demonstrates that messages travel in both directions between the parent `MissionControlComponent` and the `AstronautComponent` children, facilitated by the service:

![Parent/Children with a Service](../../../Assets/p&cServiceDemo.gif)

## Test It:
Tests click buttons of both the parent `MissionControlComponent` and the `AstronautComponent` children and verify that the history meets expectations:

```ts
//...
it('should announce a mission', () => {
  const missionControl = element(by.tagName('app-mission-control'))
  const announceButton = missionControl.all(by.tagName('button')).get(0)
  announceButton.click()
    .then(() => {
      const history = missionControl.all(by.tagName('li'))

      expect(history.count()).toBe(1)
      expect(history.get(0).getText()).toMatch(/Mission.* announced/)
    })
})

it('should confirm the mission by Lovell', () => {
  testConfirmMission(1, 2, 'Lovell')
})

it('should confirm the mission by Haise', () => {
  testConfirmMission(3, 3, 'Haise')
})

it('should confirm the mission by Swigert', () => {
  testConfirmMission(2, 4, 'Swigert')
})

function testConfirmMission(buttonIndex: number, expectedLogCount: number, astronaut: string) {
  const _confirmedLog: string = ' confirmed the mission'
  const missionControl = element(by.tagName('app-mission-control'))
  const confirmButton = missionControl.all(by.tagName('button')).get(buttonIndex)
  confirmButton.click()
    .then(() => {
      const history = missionControl.all(by.tagName('li'))

      expect(history.count()).toBe(expectedLogCount)
      expect(history.get(expectedLogCount--).getText()).toBe(astronaut + _confirmedLog)
    })
}
//...
```

---

[Angular Docs](https://angular.io/guide/component-interaction#parent-and-children-communicate-via-a-service)