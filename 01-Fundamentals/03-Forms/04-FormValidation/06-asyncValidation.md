##### 4/24/2020
# Form Validation - Async Validation
This section shows how to create asynchronous validators.  It assumes some basic knowledge of creating custom validators. 

---

## The Basics:
Just like synchronous validators have the `ValidatorFn` and `Validator` interfaces, asynchronous validators have their own counterparts: `AsyncValidatorFn` and `AsyncValidator`.

They are very similar with the only difference being:
  * They must return a `Promise` or an `Observable`
  * The `Observable` returned must be finite, meaning it must complete at some point.  To convert an infinite `Observable` into a finite one, pipe the `Observable`  through a filtering operator such as `first`, `last`, `take` or `takeUntil`

It is important to note that the asynchronous validation happens after the synchronous validation, and is performed only if the synchronous validation is successful.  This check allows forms to avoid potentially expensive async validation processes such as an HTTP request if more basic validation methods fail.

After asynchronous validation begins, the form control enters a `pending` state.  You can inspect the control's `pending` property and use it to give visual feedback about the ongoing validation.

A common UI pattern is to show a spinner while the async validation is being performed.  the following example presents how to achieve this with template-driven forms:

```html
<input
  [(ngModel)]="name"
  #modal="ngModel"
  appSomeAsyncValidator
>
<app-spinner *ngIf="model.pending"></app-spinner>
```

---

## Implementing Custom Async Validator:
In the following section, validation is performed asynchronously to ensure that our heroes pick an alter ego that is not already taken.  New heroes are constantly enlisting and old heroes are leaving the service.  That means that we do not have the list of available alter egos ahead of time.

To validate the potential alter ego, we need to consult a central database of all currently enlisted heroes.  The process is asynchronous, so we need to special validator for that.

Let's start by creating the validator `class`:

```ts
@Injectable({ providedIn: 'root' })
export class UniqueAlterEgoValidator implements AsyncValidator {
  constructor(private heroesService: HeroesService) { }

  validate(
    ctrl: AbstractControl
  ): Promise<ValidationErrors | null> | Observable<ValidationErrors | null> {
    return this.heroesService.isAlterEgoTaken(ctrl.value).pipe(
      map(isTaken => (isTaken ? { uniqueAlterEgo: true } : null)),
      catchError(() => of(null))
    );
  }
}
```

As you can see, the `UniqueAlterEgoValidator` class implements the `AsyncValidator` interface.  In the constructor, we inject the `HeroesService` that has the following interface:

```ts
interface HeroesService {
  isAlterEgoTaken: (alterEgo: string) => Observable<boolean>;
}
```

In a real world application, the `HeroesService` is responsible for making an HTTP request to the hero database to check if the alter ego is available.  From the validator's point of view, the actual implementation of the service is not important, so we can just code against the `HeroesService` interface.

As the validation begins, the `UniqueAlterEgoValidator` delegates to teh `HeroesService` `isAlterEgoTaken()` method with the current control value.  At this point the control is marked as `pending` and remains in this state until the observable chains returned from the `validate()` method completes.

The `isAlterEgoTaken()` method dispatches as HTTP request that checks if the alter ego is available, the returns `Observable<boolean>` as the result.  We pipe the response through the `map` operator and transform it into a validation result.  As always, we return `null` if the form is valid, and `ValidationErrors` if it is not.  We make sure to handle any potential errors with the `catchError` operator.

Here we decided that `isAlterEgoTaken()` error is treated as a successful validation, because failure to make a validation request does not necessarily mean that the alter ego is invalid. You could handle the error differently and return the `ValidationError` object instead.

After some time passes, the observable chain completes and the async validation is done. The `pending` flag is set to `false`, and the form validity is updated.

--- 

## Note On Performance:
By default, all validators are run after every form value change. With synchronous validators, this will not likely have a noticeable impact on application performance. However, it's common for async validators to perform some kind of HTTP request to validate the control. Dispatching an HTTP request after every keystroke could put a strain on the backend API, and should be avoided if possible.

We can delay updating the form validity by changing the `updateOn` property from change (default) to `submit` or `blur`.

With template-driven forms:

```html
<input [(ngModel)]="name" [ngModelOptions]="{updateOn: 'blur'}">
```

With reactive forms:

```ts
new FormControl('', { updateOn: 'blur' });
```

---

[Angular Docs](https://angular.io/guide/form-validation#async-validation)