##### 3/19/2020
# Reactive Forms - Partial Model Updates
When updating the value for a form group instance that contains multiple controls, you may only want to update parts of the model.  This section covers how to update specific parts of a form control data model.

## Patching The Model Value:
There are two ways to update the model value:
  * Use the `setValue()` method to set a new value for an individual control.  The `setValue()` method strictly adheres to the structure of the form group and replaces the entire value for the control
  * Use the `patchValue()` method to replace any properties defined in the `object` that have changed in the form model

The strict checks of the `setValue()` method help catch nesting errors in complex forms, while `patchValue()` fails silently on those errors.

In `ProfileEditorComponent`, use the `updateProfile()` method with the example below to update the first name and street address for the user.

```ts
updateProfile() {
  this.profileForm.patchValue({
    firstName: 'Nancy', 
    address: {
      street: '123 Drew Street'
    }
  });
}
```

Simulate an update by adding a button to the template to update the user profile on demand.

```html
<p>
  <button (click)="updateProfile()">Update Profile</button>
</p>
```

When a user clicks the button, the `profileForm` model is updated with new values for `firstName` and `street`.  Notice that `street` is provided in an `object` inside the `address` property.  This is necessary because the `patchValue()` method applies the update against the model structure.  `PatchValue()` only updates properties that the form model defines.

---

[Angular Docs](https://angular.io/guide/reactive-forms#creating-nested-form-groups)