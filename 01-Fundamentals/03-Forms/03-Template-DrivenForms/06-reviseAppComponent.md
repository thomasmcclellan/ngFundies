##### 3/31/2020
# Template-Driven Forms - Revise `app.component.html`
`AppComponent` is the application's root component.  It will host the new `HeroFormComponent`.

Replace the contents of its template with the following:

```html
<app-hero-form></app-hero-form>
```

  > There are only two changes.  The `template` is simply the new element tag identified by the component's `selector` property.  This displays the hero form when the application component is loaded.  Don't forget to remove the `name` field the class body as well.

---

[Angular Docs](https://angular.io/guide/forms#revise-appcomponenthtml)