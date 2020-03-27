##### 3/26/2020
# Template-Driven Forms - Create The Hero Model Class
As users enter form data, you'll capture their changes and update an instance of the model.  You can't lay out the form until you know what the model looks like.

A model can be as simple as a 'property bag' that holds facts about a thing of application importance.  That describes well the `Hero` class with its three required fields (`id`, `name`, `power`) and one optional field (`alterEgo`).

Using the `Angular` CLI command `ng g c`, generate a new class named `Hero`:

```
ng g c Hero
```

With this content:

```ts
export class Hero {
  constructor(
    public id: number,
    public name: string,
    public power: string,
    public alterEgo?: string
  ) { }
}
```

It's an anemic model with few requirements and no behavior.  Perfect for the demo.

The `TS` compiler generates a public field for each `public` constructor and automatically assigns the parameter's value to that field when you create heroes.

The `alterEgo` is optional, so the constructor lets you omit it; not the question mark in `alterEgo?`.

You can create a new hero like this:

```ts
const myHero = new Hero(
  42, 
  'SkyDog', 
  'Fetch any object at any distance', 
  'Leslie Rollover'
);

console.log('My hero is called ' + myHero.name); // My hero is called SkyDog
```

---

[Angular Docs](https://angular.io/guide/forms#create-the-hero-model-class)