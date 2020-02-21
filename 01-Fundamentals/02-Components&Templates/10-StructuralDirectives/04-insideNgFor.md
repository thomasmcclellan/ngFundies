##### 2/11/2020
# Structural Directives - Inside `*ngFor`
`Angular` transforms the `*ngFor` in similar fashion from the asterisk syntax (`*ngFor`) to `<ng-template>` _element_.

Here's a full-featured application for `NgFor`, written both ways:

```html
<div 
  *ngFor="let hero of heroes; let i=index; let odd=odd; trackBy: trackById" 
  [class.odd]="odd"
>
  ({{ i }}) {{ hero.name }}
</div>

<ng-template
  ngFor
  let-hero
  [ngForOf]="heroes"
  let-i="index"
  let-odd="odd"
  [ngForTrackBy]="trackById"
>
  <div [class.odd]="odd">({{ i }}) {{ hero.name }}</div>
</ng-template>
```

This is manifestly more complicated than `ngIf` and rightly so.  The `NgFor` directive has more features, both required and optional, than the `NgIf` shown in this guide.  At minimum, `NgFor` needs a looping variable (`let hero`) and a list (`heroes`).

You enable these features in the `string` assigned to `ngFor`, which you write in `Angular`'s **microsyntax**.

  > Everything _outside_ the `ngFor` `string` stays with the host element (the `<div>`) as it moves inside the `<ng-template>`.  In this example, the `[ngClass]="odd"` stays on the `<div>`.

---

[Angular Docs](https://angular.io/guide/structural-directives#inside-ngfor)