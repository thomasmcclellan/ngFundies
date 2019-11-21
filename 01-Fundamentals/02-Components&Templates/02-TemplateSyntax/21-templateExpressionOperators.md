##### 11/21/2019
# Template Syntax - Template Expression Operators
The `Angular` template expression language employs a subset of `JS` syntax supplemented with a few special operators for specific scenarios.  The next sections cover three of these operators:
  * Pipe Operators
  * Safe Navigation Operators
  * Non-Null Assertion Operators

## The Pipe Operator (`|`):
The result of an expression might require some transformation before you're ready to use it in a binding.  For example, you might display a number as a currency, change text to uppercase, or filter a list and sort it.

Pipes are simple `functions` that accept an input value and return a transformed value.  They're easy to apply within template expressions, using the pipe operator (`|`).

```html
<p>Title through uppercase pipe: {{ title | uppercase }}</p>
```

The pipe operator passes the result of an expression on the left to a pipe `function` on the right.

You can chain expressions through multiple pipes:

```html
<!-- Convert title to uppercase, then to lowercase-->
<p>Title through a pipe chain: {{ title | uppercase | lowercase }}</p>
```

You can also [apply parameters](https://angular.io/guide/pipes#parameterizing-a-pipe) to a pipe:

```html
<p>Item json pipe: {{ item | json }}</p>
```

The generated output would look something like this:

```json
{
  "name": "Telephone",
  "manufactureDate": "1980-02-25T05:00:00.000Z",
  "price": 98
}
```

  > The pipe operator has a higher precedence than the ternary operator (`?:`), which means `a ? b : c | x` is parsed as `a ? b : (c | x)`.  Nevertheless, for a number of reasons, the pipe operator cannot be used without parentheses in the first and second operands of `?:`.  A good practice is to use parentheses in the third operand too.

## The Safe Navigation Operator (`?`) and Null Property Paths:
The `Angular` safe navigation operator, `?`, guards against `null` and `undefined` values in property paths.  Here, it protects against a view render failure if `item` is `null`.

```html
<p>The item name is: {{ item?.name }}</p>
```

If `item` is `null`, the view still renders but the displayed value is bland; you see only `'The item name is:'` with nothing after it.

Consider the next example, with `nullItem`:

```
The null item name is {{ nullItem.name }}
```

Since there is no safe navigation operator and `nullItem` is `null`, `JS` and `Angular` would throw a `null` reference error and break the rendering process of `Angular`.

```
TypeError: Cannot read property 'name' of null.
```

Sometimes however, `null` values in the property path may be ok under certain circumstances, especially when the value starts out `null` but the data arrives eventually.

With the safe navigation operator, `?`, `Angular` stops evaluating the expression when it hits the first `null` value and renders the view without errors.

It works perfectly with long property paths such as `a?.b?.c?.d`.

## The Non-Null Assertion Operator (`!`):
As of `TypeScript 2.0`, you can enforce [strict null checking](http://www.typescriptlang.org/docs/handbook/release-notes/typescript-2-0.html) with the `--strictNullChecks` flag.  `TS` then ensures that no variable is unintentionally `null` or `undefined`.

In this mode, typed variables disallow `null` and `undefined` by default.  The type checker throws an error if you leave a variable unassigned or try to assign `null` or `undefined` to a variable whose type disallows `null` or `undefined`.

The type checker also throws an error if it can't determine whether a variable will be `null` or `undefined` at runtime.  You tell the type checker not to throw an error by applying the postfix [non-null assertion operator, `!`](http://www.typescriptlang.org/docs/handbook/release-notes/typescript-2-0.html#non-null-assertion-operator).

The `Angular` non-null assertion operator, `!`, serves the same purpose in an `Angular` template.  For example, after you use `*ngIf` to check that `item` is defined, you can assert that `item` properties are also defined.

```html
<!--No color, no error-->
<p *ngIf="item">The item's color is: {{ item!.color }}</p>
```

When the `Angular` compiler turns your template into `TS` code, it prevents `TS` from reporting that `item` might be `null` or `undefined`.

Unlike the safe navigation operator, the non-null assertion operator does not guard against `null` or `undefined`.  Rather, it tells the `TS` type checker to suspend strict `null` checks for a specific property expression.

The non-null assertion operator, `!`, is optional with the exception that you must use it when you turn on strict `null` checks

---

[Angular Docs](https://angular.io/guide/template-syntax#template-expression-operators)