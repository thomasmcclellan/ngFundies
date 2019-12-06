##### 12/06/2019
# User Input - Put It All Together
Now, put it all together in a micro-app that can display a list of heroes and add new heroes to the list.  The user can add a hero by typing the hero's name in the input box and clicking **Add**.

![User Input Together](../../../Assets/userInputTogetherDemo.gif)

Below, is the 'Little Tour of Heroes' component.

```ts
@Component({
  selector: 'app-little-tour',
  template: `
    <input
      #newHero
      (keyup.enter)="addHero(newHero.value)"
      (blur)="addHero(newHero.value); newHero.value=''"
    >
    <button (click)="addHero(newHero.value)">Add</button>

    <ul><li *ngFor="let hero of heroes">{{ hero }}</li></ul>
  `
})
export class LittleTourComponent {
  heroes: string[] = ['Windstorm', 'Bombasto', 'Magneta', 'Tornado']

  addHero(newHero: string) : void {
    if (newHero)
      this.heroes.push(newHero)
  }
}
```

### Observations:
  * **Use template variables to refer to elements**: `newHero` template variable refers to teh `<input>` element.  You can reference `newHero` from any sibling or child of the `<input>` element
  * **Pass values, not elements**: instead of passing the `newHero` into the component's `addHero` method, get the input box value and pass _that_ to `addHero`
  * **Keep template statements single**: `(blur)` event is bound to two `JS` statements:
    1. The first statement calls `addHero`
    2. The second statement, `newHero.value=''` clear the input box after a new hero is added to the list

  > **NOTE**: These techniques are useful for small-scale demonstrations, but they quickly become verbose and clumsy when handling large amounts of user input.  Two-way data binding is a more elegant and compact way to move values between data entry fields and model properties. 

---

[Angular Docs](https://angular.io/guide/user-input#put-it-all-together)