##### 2/27/2020
# Pipes - Next Steps
Pipes are a great way to encapsulate and share common display-value transformations.  Use them like styles, dropping them into your template's expressions to enrich the appeal and usability of your views.

  > Explore `Angular`'s inventory of built-in pipes in the [API Reference](https://angular.io/api?type=pipe).  Try writing a custom pipe and perhaps contributing it to the community.

## Appendix: No _FilterPipe_ or _OrderByPipe_:
`Angular` doesn't provide pipes for filtering or sorting lists.  Developers familiar with `AngularJS` know these as `filter` and `orderBy`.  There is no equivalent in `Angular`.

This isn't an oversight.  `Angular` doesn't offer such pipes because they perform poorly and prevent aggressive minification. Both `filter` and `orderBy` require parameters that reference `object` properties.  Earlier in this page, you learned that such pipes must be _impure_ and that `Angular` calls impure pipes in almost every change-detection cycle.

Filtering and especially sorting are expensive operations.  The user experience can degrade severely for even moderate-sized lists when `Angular` calls these pipe methods many times per second.  `filter` and `orderBy` have often been abused in `AngularJS` apps, leading to complaints that `Angular` itself is slow.  That charge is fair in the indirect sense that `AngularJS` prepared this performance trap by offering `filter` and `orderBy` in the first place.

The minification hazard is also compelling, if less obvious.  Imagine a sorting pipe applied to a list of heroes.  The list might be sorted by hero `name` and `planet` of origin properties in the following way:

```html
<!-- Not real code -->
<div *ngFor="let hero of heroes | orderBy: 'name, planet'"></div>
```

You identify the sort fields by text `strings`, expecting the pipe to reference a property value by indexing (such as `hero['name']`).  Unfortunately, aggressive minification manipulates the `Hero` property names so that `Hero.name` and `Hero.planet` becomes something like `Hero.a` and `Hero.b`.  Clearly `hero['name']` doesn't work.

Wile some may not care to minify this aggressively, the `Angular` product shouldn't prevent anyone from minifying aggressively.  Therefore, the `Angular` team decided that everything `Angular` provides will minify safely.

The `Angular` team and many experienced `Angular` developers strongly recommend moving filtering and sorting logic into the component itself.  The component can expose a `filteredHeroes` or `sortedHeroes` property and take control over when and how often to execute the supporting logic.  Any capabilities that you would have put in a pipe and shared across the app can be written in a filtering/sorting service and injected into the component.

If these performance and minification considerations don't apply to you, you can always create your own such pipe (similar to the `FlyingHeroesPipe`) or find them in the community.
  
---

[Angular Docs](https://angular.io/guide/pipes#next-steps)