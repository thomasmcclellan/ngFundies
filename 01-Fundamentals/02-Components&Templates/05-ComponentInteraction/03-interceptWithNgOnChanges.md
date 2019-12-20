##### 12/20/2019
# Component Interaction - Intercept Input Property Changes With `ngOnChanges()`
Detect and act upon changes to input property values with the `ngOnChanges()` method of the `OnChanges` lifecycle hook interface.

  > You may prefer this approach to the property setter when watching multiple, interacting input properties.

This `VersionChildComponent` detects changes to the `major` and `minor` input properties and composes a log message reporting these changes:

```ts
import { Component, Input, OnChanges, SimpleChange } from '@angular/core';

@Component({
  selector: 'app-version-child',
  template: `
    <h3>Version {{ major }}.{{ minor }}</h3>
    <h4>Change log:</h4>
    <ul>
      <li *ngFor="let change of changeLog">{{ change }}</li>
    </ul>
  `
})
export class VersionChildComponent implements OnChanges {
  @Input() major: number
  @Input() minor: number
  
  changeLog: string[] = []

  ngOnChanges(changes: { [propKey: string]: SimpleChange }): void {
    let log: string[] = []

    for (let propName in changes) {
      let changedProp = changes[propName]
      let to = JSON.stringify(changedProp.currentValue)

      if (changedProp.isFirstChange()) {
        log.push(`Initial value of ${propName} set to ${to}`)
      } else {
        let from = JSON.stringify(changedProp.previousValue)
        log.push(`${propName} changed from ${from} to ${to}`)
      }
    }
    
    this.changeLog.push(log.join(', '))
  }
}
```

The `VersionParentComponent` supplies the `minor` and `major` values and binds buttons to methods that change them.

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-version-parent',
  template: `
    <h2>Source code version</h2>
    <button (click)="newMinor()">New minor version</button>
    <button (click)="newMajor()">New major version</button>
    <app-version-child
      [major]="major"
      [minor]="minor"
    ></app-version-child>
  `
})
export class VersionParentComponent {
  minor: number = 1
  major: number = 23

  newMinor() {
    this.minor++
  }

  newMajor() {
    this.major++
    this.minor = 0
  }
}
```

Here's the output of a button-pushing sequence:

<!-- ![Intercept with `ngOnChanges()`](../../../Assets/interceptWithOnChangesDemo.gif) -->

## Test It:
Test that _both_ input properties are set initially and that button clicks trigger the expected `ngOnChanges()` calls and values:

```ts
// ...
// Test must all execute in this exact order
it ('should set expected initial values', () => {
  const actual = getActual()
  const initialLabel: string = 'Version 1.23'
  const initialLog: string = 'Initial value of major set to 1, Initial value of minor set to 23'

  expect(actual.label).toBe(initialLabel)
  expect(actual.count).toBe(1)
  expect(actual.logs.get(0).getText()).toBe(initialLog)
})

it ('should set expected values after clicking \'Minor\' twice', () => {
  const repoTag = element(by.tagName('app-version-parent'));
  const newMinorButton = repoTag.all(by.tagName('button')).get(0);

  newMinorButton.click().then(() => {
    newMinorButton.click().then(() => {
      const actual = getActual();

      const labelAfter2Minor: string = 'Version 1.25';
      const logAfter2Minor: string = 'minor changed from 24 to 25';

      expect(actual.label).toBe(labelAfter2Minor);
      expect(actual.count).toBe(3);
      expect(actual.logs.get(2).getText()).toBe(logAfter2Minor);
    });
  });
})

it('should set expected values after clicking \'Major\' once', () => {
  const repoTag = element(by.tagName('app-version-parent'));
  const newMajorButton = repoTag.all(by.tagName('button')).get(1);

  newMajorButton.click().then(() => {
    const actual = getActual();

    const labelAfterMajor: string = 'Version 2.0';
    const logAfterMajor: string = 'Major changed from 1 to 2, minor changed from 25 to 0';

    expect(actual.label).toBe(labelAfterMajor);
    expect(actual.count).toBe(4);
    expect(actual.logs.get(3).getText()).toBe(logAfterMajor);
  });
});

function getActual() {
  const versionTag = element(by.tagName('app-version-child'));
  const label = versionTag.element(by.tagName('h3')).getText();
  const ul = versionTag.element((by.tagName('ul')));
  const logs = ul.all(by.tagName('li'));

  return {
    label: label,
    logs: logs,
    count: logs.count()
  };
}
// ...
```

---

[Angular Docs](https://angular.io/guide/component-interaction#intercept-input-property-changes-with-ngonchanges)