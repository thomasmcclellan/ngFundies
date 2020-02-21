##### 2/07/2020
# Structural Directives - `NgIf` Case Study
`NgIf` is the simplest structural directive and the easiest to understand.  It takes a `boolean` expression and makes an entire chunk of the `DOM` appear or disappear.

```html
<p *ngIf="true">Expression is true and ngIf is true.  This paragraph is in the DOM.</p>
<p *ngIf="false">Expression is false and ngIf is false.  This paragraph is not in the DOM.</p>
```

The `ngIf` directive doesn't hide elements with `CSS`; it adds/removes them physically from the `DOM`.  Confirm that fact using browser developer tools to inspect the `DOM`.

![`ngIf` Browser Dev Tool Check](../../../Assets/ngIfBrowserCheck.png)

The top paragraph is in the `DOM`, the bottom, disused paragraph is not.  In this place, is a comment about 'bindings'.

When the condition is `false`, `NgIf` removes its host element from the `DOM`, detaches it from `DOM` events (the attachments that it made), detaches the component from `Angular` change detection, and destroys it.  The component and `DOM` nodes can be garbage-collected and free up memory.

## Why _Remove_ Rather Than _Hide_?:
A directive could hide the unwanted paragraph instead by setting its `display` style to none.

```html
<p [style.display]="'block'">Expression sets display to 'block'.  This paragraph is visible.</p>
<p [style.display]="'none'">Expression sets display to 'non'.  This paragraph is hidden but still in the DOM.</p>
```

While invisible the element remains in the DOM.

![`ngIf` Browser Dev Tool Check](../../../Assets/ngIfBrowserCheck2.png)

The difference between hiding and removing doesn't matter for a simple paragraph.  It does matter when the host element is attached to a resource intensive component.  Such a component's behavior continues even when hidden.  The component stays attached to its `DOM` element.  It keeps listening to events.  `Angular` keeps checking for changes that could affect data bindings.  Whatever the component was doing, it keeps doing.

Although invisible, the component--and all of its descendant components--tie up resources.  The performance and memory burden can be substantial, responsiveness can degrade, adn the user sees nothing.

On the positive side, showing the element again is quick.  The component's previous state is preserved and ready to display.  The component doesn't re-initialize--an operation that could be expensive.  So hiding and showing is sometimes the right things to do.

But in the absence of a compelling reason to keep them around, your preference should be to remove the `DOM` elements that the user can't see and recover the unused resources with a structural directive like `NgIf`.

**These same considerations apply to every structural directive, whether built-in or custom**.  Before applying a structural directive, you might want to pause for moment to consider the consequences of adding/removing elements and of creating/destroying components.

---

[Angular Docs](https://angular.io/guide/structural-directives#ngif-case-study)