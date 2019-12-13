##### 12/09/2019
# Lifecycle Hooks - Interfaces Are Optional (Technically)
The interfaces are optional for `JS` and `TS` developers from a purely technical perspective.  The `JS` language doesn't have interfaces at all.  `Angular` can't see `TS` interfaces at runtime because they disappear from the transpiled `JS`.

Fortunately, they aren't necessary.  You don't have to add the lifecycle hook interface to directives and components to benefit from the hooks themselves.

`Angular`, instead, inspects directive and component classes and calls the hook methods _if they are defined_.  `Angular` fines and calls methods like `ngOnInit()`, with or without the interfaces.  

Nonetheless, it is good practice to add interfaces to `TS` directive classes in order to benefit from strong typing and editor tooling.

---

[Angular Docs](https://angular.io/guide/lifecycle-hooks#interfaces-are-optional-technically)