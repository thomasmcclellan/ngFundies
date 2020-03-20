##### 2/24/2020
# Pipes - Chaining Pipes
You can chain pipes together in potentially useful combinations.  In the following example, to display the birthday in uppercase, the birthday is chained to the `DatePipe` and on to the `UpperCasePipe`.  The birthday displays as `APR 15, 1988`.

```html
<p>The chained hero's birthday is {{ birthday | date | uppercase }}</p>
```

This example--which displays `FRIDAY, APRIL 15, 1988`--chains the same pipes as above, but passes in a parameter to date as well.

```html
<p>The chained hero's birthday is {{ birthday | date:'fullDate' | uppercase }}</p>
```

---

[Angular Docs](https://angular.io/guide/pipes#chaining-pipes)