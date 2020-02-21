##### 2/11/2020
# Structural Directives - Microsyntax
The `Angular` microsyntax lets you configure a directive in a compact, friendly `string`.  The microsyntax parser translates that `string` into attributes on the `<ng-template>`:
  * The `let` keyword declares a [template input variable](https://angular.io/guide/structural-directives#template-input-variable) that you reference within the template.  The input variables in this example are `hero`, `i`, and `odd`.  The parser translates `let hero`, `let i` and `let odd` into variables named `let-hero`, `let-i`, and `let-odd`.
  * The microsyntax parser title-cases all directives and prefixes them with the directive's attribute name, such as `ngFor`.  For example, the `ngFor` input properties, `of` and `trackBy`, become `ngForOf` and `ngForTrackBy`, respectively.  That's how the directive learns that the list is `heroes` and the track-by `function` is `trackById`.
  * As the `NgFor` directive loops through the list, it sets and resets properties of its own _context_ `object`.  These properties can include, but aren't limited to, `index`, `odd` and a special property named `$implicit`.
  * The `let-i` and `let-odd` variables were defined as `let i="index"` and `let odd="odd"`.  `Angular` sets them to the current value of the context's `index` and `odd` properties.
  * The context property for `let-hero` wasn't specified.  Its intended source is implicit.  `Angular` sets `let-hero` to the value of the context's `$implicit` property, which `NgFor` has initialized with the `hero` for the current iteration.
  * The `NgFor` [API guide](https://angular.io/api/common/NgForOf) describes additional `NgFor` directive properties and context properties.
  * The `NgForOf` directive implements `NgFor`.  Read more about additional `NgForOf` directive properties and context properties in the [`NgForOf` API reference](https://angular.io/api/common/NgForOf).

## Writing Your Own Structural Directives:
These microsyntax mechanisms are also available to you when you write your own structural directive.  For example, microsyntax in `Angular` allows you to write `<div *ngFor="let item of items">{{ item }}</div>` instead of `<ng-template ngFor let-item [ngForOf]="items"><div>{{ item }}</div></ng-template>`.  The following sections provide detailed information on constraints, grammar, adn translation of microsyntax.

## Constraints:
Microsyntax must meet the following requirements:
  * It must be known ahead of time so that IDEs can parse it without knowing the underlying semantics of the directive or what directives are present
  * It must translate to key-value attributes in the `DOM`

## Grammar:
When you write your own structural directives, use the following grammar:

```
*:prefix="( :let | :expression) (';' | ',')? ( :let | :as | :keyExp)*"
```

The following tables describe each portion of the microsyntax grammar:

| Attribute | Description |
|---|---|
| `prefix` | `HTML` attribute key |
| `key` | `HTML` attribute key |
| `local` | Local variable name used in the template |
| `export` | Value exported by the directive under a given name |
| `expression` | Standard `Angular` expression |

||
|---|
| `keyExp = :key ":"? :expression ("as" :local)? ";"?` |
| `let = "let" :local "=" :export ";"?` |
| `as = :export "as" :local ";"?` |

## Translation:
A microsyntax is translated to the normal binding syntax as follows:

| Microsyntax | Translation |
|---|---|
| `prefix` and naked `expression` | `[prefix]="expression"` |
| `keyExp` | `[prefixKey] "expression" (let-prefixKey="export")`<br>Notice that the `prefix` is added to the `key` |
| `let` | `let-local="export"` |

## Microsyntax Examples:
The following table demonstrates how `Angular` desugars microsyntax:

| Microsyntax | Desugared |
|---|---|
| `*ngFor="let item of [1,2,3]"` | `<ng-template ngFor let-item [ngForOf]="[1,2,3]">` |
| `*ngFor="let item of [1,2,3] as items; trackBy; myTrack; index as i"` | `<ng-template ngFor let-item [ngForOf]="[1,2,3]" let-items="ngForOf" [ngForTrackBy]="myTrack" let-i="index">` |
| `*ngIf="exp"` | `<ng-template [ngIf]="exp">` |
| `*ngIf="exp as value"` | `<ng-template [ngIf]="exp" let-value="ngIf">` |

  > Studying the [source code](https://github.com/angular/angular/blob/master/packages/common/src/directives/ng_if.ts) for `NgIf` and `NgForOf` is a great way to learn more.

---

[Angular Docs](https://angular.io/guide/structural-directives#microsyntax)