##### 9/30/2019
# Introduction to Displaying Data - Creating a Class for the Data
The app's code defines the data directly inside the component, which isn't best practice.  In a simple demo, however, it is fine.

At the moment, the binding is to an array of strings.  In real applications, most bindings are to more specialized objects.

To convert this binding to use specialized objects, turn the array of hero names into an array of `Hero` objects.  For that you'll need a `Hero` class.

```
ng generate class hero
```

With the following code:

`src/app/hero.ts`:
```typescript
export class Hero {
  constructor(
    public id: number,
    public name: string
  ) { }
}
```

You've defined a class with a constructor and two properties: `id` and `name`.

It might not look like the class has properties, but it does.  The declaration of the constructor parameters take advantage of the `TS` shortcut.

Consider the first parameter:

`src/app/hero.ts` (id):
```typescript
public id: number
```

That brief syntax does a lot:
  * Declares a constructor parameter and its type
  * Declares a public property of the same name
  * Initializes that property with the corresponding argument when creating an instance of the class

### Using the `Hero` Class:
After importing the `Hero` class, the `AppComponent.heroes` property cna return a _typed_ array of `Hero` objects.

`src/app/app.component.ts` (heroes):
```typescript
heroes = [
  new Hero(1, 'Windstorm')
  new Hero(13, 'Bombasto')
  new Hero(15, 'Magneta')
  new Hero(20, 'Tornado')
]

myHero = this.heroes[0]
```

Next, update the template.  At the moment it displays the hero's `id` and `name`.  Fix that to display only the hero's `name` property.

`src/app/app.component.ts` (template):
```typescript
template: `
  <h1>{{ title }}</h1>
  <h2>My favorite hero is: {{ myHero.name }}</h2>
  <p>Heroes:</p>
  <ul>
    <li *ngFor="let hero of heroes">
      {{ hero.name }}
    </li>
  </ul>
`
```

The display looks the same, but the code is cleaner.

---

[Angular Docs](https://angular.io/guide/displaying-data)