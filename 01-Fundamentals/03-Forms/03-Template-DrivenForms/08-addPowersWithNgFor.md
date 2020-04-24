##### 4/02/2020
# Template-Driven Forms - Add Powers with `*ngFor`
The hero must choose one superpower from a fixed list of agency-approved powers.  You maintain that list internally (in `HeroFormComponent`).

You'll add a `select` to the form and bind the options to the `powers` list using `ngFor`, a technique seen previously in the _Displaying Data_ section.

Add the following `HTML` _immediately below_ the _Alter Ego_ group:

```html
<div class="form-group">
  <label for="power">Hero Power</label>
  <select 
    class="form-control" 
    id="power"
    required
  >
    <option *ngFor="let pow of powers" [value]="pow">{{ pow }}</option>
  </select>
</div>
```

This code repeats the `<option>` tag for each power in the list of powers.  The `pow` template input variable is a different power in each iteration; you display its name using the interpolation syntax.

---

[Angular Docs](https://angular.io/guide/forms#add-powers-with-ngfor)