##### 12/06/2019
# Lifecycle Hooks - Overview
A component has a lifecycle managed by `Angular`.

`Angular` creates and renders components along with their children, checks when their data-bound properties change, and destroys them before removing them from the `DOM`.

`Angular` offers **lifecycle hooks** that provide visibility into these key life moments and the ability to act when they occur.

A directive has the same set of lifecycle hooks.

## Component Lifecycle Hooks Overview:
Directive and component instances have a lifecycle as `Angular` creates, updates, and destroys them.  Developers can tap into key moments in that lifecycle by implementing one or more of the _lifecycle hook_ interfaces in the `Angular` `core` library.

Each interface has a single hook method whose name is the interface name prefixed with `ng`.  For example, the `OnInit()` that `Angular` calls shortly after creating the component:

```ts
export class PeekABoo implments OnInit {
  constructor(private logger: LoggerService) { }

  // Implement OnInit's `ngOnInit` method
  ngOnInit() { this.logIt(`OnInit`) }

  logIt(msg: string) : void {
    this.logger.log(`#${nextId++} ${msg}`)
  }
}
```

No directive or component will implement all of the lifecycle hooks.  `Angular` only calls a directive/component hook method _if it is defined_.

---

[Angular Docs](https://angular.io/guide/lifecycle-hooks)