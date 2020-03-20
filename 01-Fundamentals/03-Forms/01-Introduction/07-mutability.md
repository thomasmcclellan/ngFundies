##### 3/09/2020
# Forms Introduction - Mutability
The change tracking method plays a role in the efficiency of your application
  * **Reactive forms** keeps the data model pure by providing it as an immutable data structure.  Each time a change is triggered on the data model, the `FormControl` instance returns a new data model rather than updating the existing data model.  This gives you the ability to track unique changes to the data model through the control's observable.  This provides one way for change detection to be more efficient because it only needs to update on unique changes.  It also follows reactive patterns tht integrate with observable operators to transform data.
  * **Template-driven forms** rely on mutability with two-way data binding to update the data model in the component as changes are made in the template. Because there are no unique changes to track on the data model when using two-way data binding, change detection is less efficient at determining when updates are required.

The difference is demonstrated in the examples above using the **favorite color** input element.
  * With reactive forms, the `FormControl` **instance** always returns a new value when the control's value is updated.
  * With template-driven forms, the **favorite color property** is always modified to its new value.
  
---

[Angular Docs](https://angular.io/guide/forms-overview#mutability)