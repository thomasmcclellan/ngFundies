##### 2/18/2020
# Structural Directives - The `<ng-template>`
The `<ng-template>` is an `Angular` element for rendering `HTML`.  It is never displayed directly.  In fact, before rendering the view, `Angular` _replaces_ the `<ng-template>` and its contents with a comment.

If there is no structural directive and you merely want to wrap some elements in an `<ng-template>`, those elements disappear.  That's the fate of the middle 'Hip' in the 'Hip! Hip! Hooray!' phrase:

```html
<p>Hip!</p>
<ng-template>
  <p>Hip!</p>
</ng-template>
<p>Hooray!</p>
```
`Angular` erases the middle 'Hip!', leaving the cheer a bit less enthusiastic.

![`<ng-template>` Demo](../../../Assets/ngTemplate.png)

A structural directive puts an `<ng-template>` to work as you'll see when you write your own structural directive.

---

[Angular Docs](https://angular.io/guide/structural-directives#the-ng-template)