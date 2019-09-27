##### 9/27/2019
# Introduction to Displaying Data - Constructor or Variable Initialization?
  > Although this example uses variable assignment to initialize the components, you could instead declare and initialize the properties using a constructor.

```typescript
export class AppComponent {
  title: string
  myHero: string

  constructor() {
    this.title = 'Tour of Heroes'
    this.myHero = 'Windstorm'
  }
}
```

---

[Angular Docs](https://angular.io/guide/displaying-data)