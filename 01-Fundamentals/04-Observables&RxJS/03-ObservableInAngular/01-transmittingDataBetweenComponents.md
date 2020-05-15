##### 5/14/2020
# `Observables` in `Angular` - Transmitting Data Between Components
`Angular` provides an `EventEmitter` class that is used when publishing values from a component through the `@Output()` decorator.  `EventEmitter` extends `RxJS` `Subject`, adding an `emit()` method so it can send arbitrary values.  When you call `emit()`, it passes the emitted value to the `next()` method of any subscribed observer.

A good example of usage can be found in the `EventEmitter` documentation.  Here is the example component that listens for open and close events:

```html
<zippy (open)="onOpen($event)" (close)="onClose($event)"></zippy>
```

Here is the component definition:

```ts
@Component({
  selector: 'zippy',
  template: `
    <div class="zippy">
      <div (click)="toggle()">Toggle</div>
      <div [hidden]="!visible">
        <ng-content></ng-content>
      </div>
    </div
  `
})
export class ZippyComponent {
  @Output() open = new EventEmitter<any>();
  @Output() close = new EventEmitter<any>();

  visible: boolean = true;

  toggle() : void {
    this.visible = !this.visible;

    if (this.visible) this.open.emit(null);
    else this.close.emit(null);
  }
}
```

---

[Angular Docs](https://angular.io/guide/rx-library#naming-conventions-for-observables)