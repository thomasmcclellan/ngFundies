##### 4/22/2020
# Form Validation - Customer Validators
Like in `Angular JS`, `Angular` automatically mirrors many control properties onto the form control element as `CSS` classes.  You can use these classes to style form control elements according to the state of the form.  The following classes are currently supported:
  * `.ng-valid`
  * `.ng-invalid`
  * `.ng-pending`
  * `.ng-pristine`
  * `.ng-dirty`
  * `.ng-untouched`
  * `.ng-touched`

The hero form uses the `.ng-valid` and `.ng-invalid` classes to set the color of each form control's border.

```css
.ng-valid[required], .ng-valid.required {
  border-left: 5px solid #42a948; /* green */
}

.ng-invalid:not(form) {
  border-left: 5px solid #a94442; /* red */
}
```

---

[Angular Docs](https://angular.io/guide/form-validation#control-status-css-classes)