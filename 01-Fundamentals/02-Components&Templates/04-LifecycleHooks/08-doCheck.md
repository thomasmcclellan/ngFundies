##### 12/13/2019
# Lifecycle Hooks - `DoCheck()`
Use the `DoCheck` hook to detect and act upon changes that `Angular` doesn't catch on its own.

  > Use this method to detect a change that `Angular` overlooked.

The `DoCheck` sample extends the `OnChanges` sample with the following `ngDoCheck()` hook:

```ts
ngDoCheck() {
  if (this.hero.name !== this.oldHeroName) {
    this.changeDetected = true
    this.changeLog.push(`DoCheck: Hero name changed to "${this.hero.name}" from "${this.oldHeroName}".`)
    this.oldHeroName = this.hero.name
  }

  if (this.power !== this.oldPower) {
    this.changeDetected = true
    this.changeLog.push(`DoCheck: Power changed to "${this.power}" from "${this.oldPower}".`)
    this.oldPower = this.power
  }

  if (this.changeDetected) {
    this.noChangeCount = 0
  } else {
    // Log that hook was called when there was no relevant change
    let count = this.noChangeCount += 1
    let noChangeMsg = `DoCheck called ${count}X when no change to hero or power.`
    if (count === 1) {
      // Add new "no change" message
      this.changeLog.push(noChangeMsg)
    } else {
      // Update last "no change" message
      this.changeLog[this.changeLog.length - 1] = noChangeMsg
    }
  }

  this.changeDetected = false
}
```

This code inspects certain _values of interest_, capturing and comparing their current state against previous values.  It writes a special message to the log when there are no substantive changes to the `hero` or the `power` so you can see how often `DoCheck` is called.  The results are illuminating:

![DoCheck](../../../Assets/doCheckDemo.gif)

While the `ngDoCheck()` hook can detect when the hero's `name` has changed, it has a frightful cost.  This hook is called with enormous frequency--after _every_ change detection cycle no matter where the change occurred.  It's called over twenty times in this example before the user can do anything!

Most of these initial checks are triggered by `Angular`'s first rendering of _unrelated data elsewhere on the page_.  Mere mousing into another `<input>` triggers a call.  Relatively few calls reveal actual changes to pertinent data.  Clearly our implementation must be very lightweight or the user experience suffers.

---

[Angular Docs](https://angular.io/guide/lifecycle-hooks#docheck)