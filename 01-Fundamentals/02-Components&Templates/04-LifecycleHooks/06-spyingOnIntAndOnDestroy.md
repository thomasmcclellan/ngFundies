##### 12/11/2019
# Lifecycle Hooks - _Spying_ `OnInit` and `OnDestroy`
Go undercover with these two spy hooks to discover when an element is initialized or destroyed.

This is the perfect infiltration job for a directive.  There heroes will never know they're being watched.

  > Pay attention to two key points:
  >   1. `Angular` calls hook methods for _directives_ as well as _components_.
  >   2. A spy directive can provide insight into a `DOM` `object` that you cannot change directly.  Obviously, you can't touch the implementation of a native `<div>`.  You can't modify a third party component either.  But you can watch both with a directive.

The sneaky spy directive is simple, consisting almost entirely of `ngOnInit()` and `ngOnDestroy()` hooks that log messages to the parent via an injected `LoggerService`.

```ts
// Spy on any element to which it is applied
// Usage: <div mySpy>...</div>
@Directive({ selector: '[mySpy]' })
export class SpyDirective implements OnInit, OnDestroy {
  constructor(private logger: LoggerService) { }

  ngOnInit() { this.logIt('onInit') }
  ngOnDestroy() { this.logIt('onDestroy') }

  private logIt(msg: string) : void {
    this.logger.log(`Spy #${nextId++} ${msg}`)
  }
}
```

You can apply the spy to any native or component element and it'll be initialized and destroyed at the same time as that element.  Here it is attached to the repeated hero `<div>`:

```html
<div 
  *ngFor="let hero of heroes"
  mySpy
  class="heroes"
>
  {{ hero }}
</div>
```

Each spy's birth and death marks the birth and death of the attached hero `<div>` with an entry in the _Hook Log_ as seen here:

![Spy Directive](../../../Assets/spyDirectiveDemo.gif)

Adding a hero results in a new hero `<div>`.  The spy's `ngOnInit()` logs that event.

The _Reset_ button clears the `heroes` list.  `Angular` removes all hero `<div>` elements from the `DOM` and destroys their spy directives at the same time.  The spy's `ngOnDestroy()` method reports its last moments.

The `ngOnInit()` and `ngOnDestroy()` methods have more vital roles to play in real applications.

## `OnInit()`:
Use `ngOnInit()` for two main reasons: 
  1. To perform complex initialization shortly after construction
  2. To set up the component after `Angular` set the input properties

Experienced developers agree that components should be cheap and safe to construct.

  > Misko Havery, `Angular` team lead, [explains](http://misko.hevery.com/code-reviewers-guide/flaw-constructor-does-real-work/) why you should avoid constructor logic.

Don't fetch data in a component constructor.  You shouldn't worry that a new component will try to contact a remote server when created under test or before you decide to display it.  Constructors should do no more than set the initial local variables to simple values.

An `ngOnInit()` is a good place for a component to fetch its initial data.

Remember also that a directive's data-bound input properties are not set until _after_ construction.  That's a problem if you need to initialize the directive based on those properties.  They'll have been set when `ngOnInit()` runs.

  > The `ngOnChanges()` method is your first opportunity to access those properties. `Angular` calls `ngOnChanges()` _before_ `ngOnInit()` and many times after that.  It only calls `ngOnInit()` once.

You can count on `Angular` to call the `ngOnInit()` method _soon_ after creating the component.  That's where the heavy initialization logic belongs.

## `OnDestroy()`:
Put cleanup logic in `ngOnDestroy()`, the logic that **must** run _before_ `Angular` destroys the directive.

This is the time to notify another part of the application that the component is going away.

This is the place to free resources that won't be garbage collected automatically:  unsubscribe from Observables and `DOM` events; stop interval timers; unregister all callbacks that this directive registered with global or application services.  **You risk memory leaks if you neglect to do so.**

  > Live example can be found [HERE](https://stackblitz.com/angular/oyxxmyyrorqe).

---

[Angular Docs](https://angular.io/guide/lifecycle-hooks#spying-oninit-and-ondestroy)