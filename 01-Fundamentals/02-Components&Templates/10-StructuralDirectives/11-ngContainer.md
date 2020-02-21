##### 2/19/2020
# Structural Directives - Group Sibling Elements With `<ng-container>`
There's often a _root_ element that can and should host the structural directive.  The list element (`<li>`) is a typical host element of an `NgFor` repeater.

```html
<li *ngFor="let hero of heroes">{{ hero.name }}</li>
```

When there isn't a host element, you can usually wrap the content in a native `HTML` container element, such as a `<div>`, and attach the directive to that wrapper.

```html
<div *ngIf="hero" class="name">{{ hero.name }}</div>
```

Introducing another container element--typically a `<span>`, or `<div>`--to group the elements under a single _root_ is usually harmless.  _Usually_...but not _always_.

The grouping element may break the template appearance because `CSS` styles neither expect nor accommodate the new layout.  For example, suppose you have the following paragraph layout:

```html
<p>
  I turned the corner
  <span *ngIf="hero">
    and saw {{ hero.name }}.  I waved
  </span>
  and continued on my way.
</p>
```

You also have a `CSS` style rule that happens to apply to a `<span>` within a `<p>` tag.

```css
p span {
  color: red;
  font-size: 70%;
}
```

The constructed paragraph renders strangely.

![Nesting issues](../../../Assets/nestingIssues.png)

The `p span` style, intended for use elsewhere, was inadvertently applied here.

Another problem:  some `HTML` elements require all immediate children to be of a specific type.  For example, the `<select>` element requires `<option>` children.  You can't wrap the _options_ in a conditional `<div>` or a `<span>`.

When you try this:

```html
<div>
  Pick your favorite hero (
    <label>
      <input 
        type="checkbox" 
        checked 
        (change)="showSad = !showSad"
      >show sad
    </label>
  )
</div>
<select [(ngModel)]="hero">
  <span *ngFor="let hero of heroes">
    <span *ngIf="showSad || hero.emotion !== 'sad'">
      <option [ngValue]="hero">{{ hero.name }} ({{ hero.emotion }})</option>
    </span>
  </span>
</select>
```

The drop down is empty.

![Spanning Issues](../../../Assets/spanningIssues.png)

The browser won't display an `<option>` within a `<span>`.

## `<ng-container>` To The Rescue:
The `Angular` `<ng-container>` is a grouping element that doesn't interfere with styles or layout because `Angular` _doesn't put it in the `DOM`_.

Here's the conditional paragraph again, this time using `<ng-container>`:

```html
<p>
  I turned the corner
  <ng-container *ngIf="hero">
    and saw {{ hero.name }}.  I waved
  </ng-container>
  and continued on my way.
</p>
```

It renders properly.

![Nesting with `<ng-container>`](../../../Assets/nestingWithNgContainer.png)

Now conditionally exclude a _select_ `<option>` with `<ng-container>`.

```html
<div>
  Pick your favorite hero (
    <label>
      <input
        type="checkbox"
        checked
        (change)="showSad = !showSad"
      >show sad
    </label>
  )
</div>
<select [(ngModel)]="hero">
  <ng-container *ngFor="let hero of heroes">
    <ng-container *ngIf="showSad || hero.emotion !== 'sad'">
      <option [ngValue]="hero">{{ hero.name }} ({{ hero.emotion }})</option>
    </ng-container>
  </ng-container>
</select>
```

The drop down works properly.

![Dropdown With `<ng-container>`](../../../Assets/dropdownWithNgContainer.gif)

  > **NOTE**: Remember that `ngModel` directive is defined as a part of `Angular` `FormsModule` and you need to include `FormsModule` in the `imports: [...]` section of the `Angular` module metadata, in which you want to use it.

The `<ng-container>` is a syntax element recognized by the `Angular` parser.  It's not a directive, component, class, or interface.  It's more like the curly braces in a `JS` `if-block`:

```js
if (someCondition) {
  statement1;
  statement2;
  statement3;
}
```

Without those braces, `JS` would only execute the first statement when you intend to conditionally execute all of them as a single block. The `<ng-container>` satisfies a similar need in `Angular` templates.

---

[Angular Docs](https://angular.io/guide/structural-directives#the-ng-template)