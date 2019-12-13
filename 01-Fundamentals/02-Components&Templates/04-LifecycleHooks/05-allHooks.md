##### 12/10/2019
# Lifecycle Hooks - _Peek-a-Boo_: All Hooks
The `PeekABooComponent` demonstrates all of the hooks in one component.

You would rarely, if ever, implement all fo the interfaces like this.  The peek-a-boo exists to show how `Angular` calls the hooks in the expected order.

This snapshot reflects the state of the log after the user clicked the _Create_ button and then the _Destroy_ button.

![Peek-a-boo](../../../Assets/peekABoo.png)

The sequence of log messages follows the prescribed hook calling order: `OnChanges`, `OnInit`, `DoCheck` (3x), `AfterContentInit`, `AfterContentChecked` (3x), `AfterViewInit`, `AfterViewChecked` (3x), and `OnDestroy`.

  > The constructor isn't an `Angular` hook _per se_.  The log confirms that input property (the `name` property in this case) have no assigned values at construction.

Had the user clicked the _Update Hero_ button, the log would show another `OnChanges` and two more triplets of `DoCheck`, `AfterContentChecked`, and `AfterViewChecked`.  

  > Clearly these three hooks (`DoCheck`, `AfterContentChecked`, and `AfterViewChecked`) fire _often_.  Keep the logic in these hooks as lean as possible!

  > Live example can be found [HERE](https://stackblitz.com/angular/oyxxmyyrorqe).

---

[Angular Docs](https://angular.io/guide/lifecycle-hooks#peek-a-boo-all-hooks)