##### 12/06/2019
# User Input - On Blur
In the previous example, the current state of the input box is lost if the user mouses away and clicks elsewhere on the page without first pressing _Enter_.  The component's `value` property is updated only when the user presses _Enter_.

To fix this issue, listen to **both** the _Enter_ key and the _blur_ event.

```ts
@Component({
  selector: 'app-key-up4',
  template: `
    <input
      #box
      (keyup.enter)="update(box.value)"
      (blur)="update(box.value)"
    >
    <p>{{ value }}</p>
  `
})
export class KeyUpComponent_V4 {
  value: string = ''

  update(value: string) : void {
    this.value = value
  }
}
```

---

[Angular Docs](https://angular.io/guide/user-input#on-blur)