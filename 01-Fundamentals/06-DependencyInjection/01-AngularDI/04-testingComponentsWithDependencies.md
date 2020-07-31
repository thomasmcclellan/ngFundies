##### 7/31/2020
# `Angular` Dependency Injection - Testing Components with Dependencies
Designing a `class` with dependency injection makes the `class` easier to test. Listing dependencies as constructor parameters may be all you need to test application parts effectively.

For example, you can create a new `HeroListComponent` with a mock service that you can manipulate under test.

```ts
const expectedHeroes = [{ name: 'A' }, { name: 'B' }],
      mockService = <HeroService> { getHeroes: () => expectedHeroes };

it ('should have heroes when HeroListComponent created' () => {
  // Pass the mock to the constructor as the Angular injector would
  const component = new HeroListComponent(mockService);

  expect(component.heroes.length)
    .toEqual(expectedHeroes.length);
});
```

---

[Angular Docs](https://angular.io/guide/dependency-injection#testing-components-with-dependencies)