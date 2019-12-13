##### 12/12/2019
# Lifecycle Hooks - `OnChanges()`
`Angular` calls its `ngOnChanges()` method whenever it detects changes to **_input properties_** of the component (or directive).  This example monitors the `OnChange` hook:

```ts
ngOnChanges(changes: SimpleChanges) : void {
  for (let propName in changes) {
    let chng = changes[propName]
    let cur = JSON.stringify(chng.currentValue)
    let prev = JSON.stringify(chng.previousValue)

    this.changeLog.push(`${propName}: currentValue = ${cur}, previousValue = ${prev}`)
  }
}
```

The `ngOnChanges()` method takes an `object` that maps each changed property name to a [SimpleChange](https://angular.io/api/core/SimpleChange) `object` holding the current and previous values.  This hook iterates over the changed properties and logs them.

The example component, `OnChangesComponent`, has two input properties: `hero` and `power`:

```ts
@Input() hero: Hero
@Input() power: string
```

The host `OnChangesParentComponent` binds to them like this:

```html
<on-changes [hero]="hero" [power]="power"></on-changes>
```
Here's the sample in action as the user makes changes:

![OnChanges](../../../Assets/onChangesDemo.gif)

The log entries appear as the `string` value of the _power_ property changes.  But the `ngOnChanges()` does not catch changes to `hero.name`.  That's surprising at first.

`Angular` only calls the hook when the value of the input property changes.  The value of the `hero` property is the _reference_ to the `hero` `object`. `Angular` doesn't care that the hero's own `name` property changed.  The `hero` `object` _reference_ didn't change so, from `Angular`'s perspective, there is no change to report.

---

[Angular Docs](https://angular.io/guide/lifecycle-hooks#onchanges)