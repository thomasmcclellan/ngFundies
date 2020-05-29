##### 5/27/2020
# Compare to Other Techniques - `Observables` Compared to `Arrays`
An `observable` produces values over time.  An `array` is created as a static set of values.  In a sense, `observables` are asynchronous where `arrays` are synchronous.  

  > **NOTE**: In the following example, `➞` implies _asynchronous_ value delivery.

## Given:
`Observables`:

```ts
	
obs: ➞1➞2➞3➞5➞7
obsB: ➞'a'➞'b'➞'c'
```

`Arrays`:

```ts
arr: [1, 2, 3, 5, 7]
arrB: ['a', 'b', 'c']
```

## `concat()`:
`Observables`:

```ts
concat(obs, obsB)
➞1➞2➞3➞5➞7➞'a'➞'b'➞'c'
```

`Arrays`:

```ts
arr.concat(arrB)
[1,2,3,5,7,'a','b','c']
```

## `filter()`:
`Observables`:

```ts
obs.pipe(filter((v) => v>3))
➞5➞7
```

`Arrays`:

```ts
arr.filter((v) => v>3)
[5, 7]
```

## `find()`:
`Observables`:

```ts
obs.pipe(find((v) => v>3))
➞5
```

`Arrays`:

```ts
arr.find((v) => v>3)
5
```

## `findIndex()`:
`Observables`:

```ts
obs.pipe(findIndex((v) => v>3))
➞3
```

`Arrays`:

```ts
arr.findIndex((v) => v>3)
3
```

## `forEach()`:
`Observables`:

```ts
obs.pipe(tap((v) => {
  console.log(v);
}))
1
2
3
5
7
```

`Arrays`:

```ts
arr.forEach((v) => {
  console.log(v);
})
1
2
3
5
7
```

## `map()`:
`Observables`:

```ts
obs.pipe(map((v) => -v))
➞-1➞-2➞-3➞-5➞-7
```

`Arrays`:

```ts
arr.map((v) => -v)
[-1, -2, -3, -5, -7]
```

## `reduce()`:
`Observables`:

```ts
obs.pipe(reduce((s,v)=> s+v, 0))
➞18
```

`Arrays`:

```ts
arr.reduce((s,v) => s+v, 0)
18
```

---

[Angular Docs](https://angular.io/guide/comparing-observables#observables-compared-to-arrays)