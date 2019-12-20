##### 12/19/2019
# Component Interaction - Intercept Input Property Changes With a Setter
Use an `@Input()` property setter to intercept and act upon a value from the parent.

The setter of the `name` input property in the child `NameChildComponent` trims the whitespace from a name and replaces an empty value with default text.

```ts
import { Component, Input } from '@angular/core';

@Component({
  selector: 'app-name-child',
  template: '<h3>"{{ name }}"</h3>'
}) 
export class NameChildComponent {
  private _name: string = ''

  @Input() 
  set name(name: string) : void {
    this._name = (name && name.trim()) || '<no name set>'
  }

  get name() : string { return this._name }
}
```

Here's the `NameParentComponent` demonstrating name variations including a name with all spaces:

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-name-parent',
  template: `
    <h2>Master controls {{ name.length }} names</h2>
    <app-name-child
      *ngFor="let name of names"
      [name]="name"
    ></app-name-child>
  `
})
export class NameParentComponent {
  // Displays 'Dr. IQ', '<no name set>', 'Bombasto'
  names: string[] = ['Dr. IQ', '  ', ' Bombasto']
}
```

![Intercepts with Setter](../../../Assets/setterInterception.png)

## Test It:
`E2E` tests of input property setter with empty and non-empty names:

```ts
// ...
it ('should display trimmed, non-empty names', () => {
  let _nonEmptyNameIndex: number = 0
  let _nonEmptyName: string = '"Dr. IQ"'
  let parent = element.all(by.tagName('app-name-parent')).get(0)
  let hero = parent.all(by.tagName('app-name-child')).get(_nonEmptyNameIndex)

  let displayName = hero.element(by.tagName('h3')).getText()

  expect(displayName).toEqual(_nonEmptyName)
})

it ('should replace empty name with default name', () => {
  let _emptyNameIndex: number = 1
  let _defaultName: string = '"<no name set>"'
  let parent = element.all(by.tagName('app-name-parent')).get(0)
  let hero = parent.all(by.tagName('app-name-child')).get(_emptyNameIndex)

  let displayName = hero.element(by.tagName('h3')).getText()

  expect(displayName).toEqual(_defaultName)
})
// ...
```

---

[Angular Docs](https://angular.io/guide/component-interaction#intercept-input-property-changes-with-a-setter)