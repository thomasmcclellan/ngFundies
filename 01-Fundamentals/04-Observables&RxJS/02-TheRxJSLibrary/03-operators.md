##### 5/13/2020
# The `RxJS` Library - Operators
Operators are `functions` that build on the `observables` foundation to enable sophisticated manipulation of collections.  For example, `RxJS` defines operators such as `map()`, `filter()`, `concat()`, and `flatMap()`.

Operators take configuration options, and they return a `function` that takes a source `observable`.  When executing this returned `function`, the operator observes the source `observable`'s emitted values, transforms them, and returns a new `observable` of those transformed values.  Here is a simple example:

```ts
import { map } from 'rxjs/operators';

const nums = of(1, 2, 3),
      squareValues = map((val: number) => val * val),
      squaredNums = squareValues(nums);

squaredNums.subscribe(x => console.log(x));

// Logs:
// 1
// 4
// 9
```

You can use _pipes_ to link operators together.  Pipes let you combine multiple `functions` into a single `function`.  The `pipe()` `function` takes as its arguments the `functions` you want to combine, and returns a new `function` that, when executed, runs the composed `functions` in sequence.

A set of operators applied to an `observable` is a recipe--that is, a set of instructions for producing the values you're interested in.  By itself, the recipe doesn't do anything.  YOu need to call `subscribe()` to produce a result through the recipe.

Here's an example:

```ts
import { filter, map } from 'rxjs/operators';

const nums = of(1, 2, 3, 4, 5);
// Create a function that accepts an Observable
const squareOddVals = pipe(
  filter((n: number) => n % 2 !-- 0),
  map(n => n * n)
);
```

The `pipe()` `function` is also a method on the `RxJS` `Observable`, so you use this shorter form to define the same operation:

```ts 
import { filter, map } from 'rxjs/operators';

const squareOdd = of(1, 2, 3, 4, 5)
  .pipe(
    filter(n => n % 2 !== 0),
    map(n => n * n)
  );

// Subscribe to get values
squareOdd.subscribe(x => console.log(x));
```

---

## Common Operators:
`RxJS` provides many operators, but only a handful are used frequently.  For a list of operators and usage examples, visit the [`RxJS` API Documentation]().

  > **NOTE**: For `Angular` apps, we prefer combining operators with pipes, rather than chaining.  Chaining is used in many `RxJS` examples.

| Area | Operators |
|---|---|
| Creation | `from`<br>`fromEvent`<br>`of` |
| Combination | `combineLatest`<br>`concat`<br>`merge`<br>`startWith`<br>`withLatestFrom`<br>`zip` |
| Filtering | `debounceTime`<br>`distinctUntilChanged`<br>`filter`<br>`take`<br>`takeUntil` |
| Transformation | `bufferTime`<br>`concatMap`<br>`map`<br>`mergeMap`<br>`scan`<br>`switchMap` |
| Utility | `tap` |
| Multicasting | `share` |

---

[Angular Docs](https://angular.io/guide/rx-library#operators)