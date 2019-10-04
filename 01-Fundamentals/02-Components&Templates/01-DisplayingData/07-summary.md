##### 10/01/2019
# Introduction to Displaying Data - Summary
Now you know how to use:
    * **Interpolation** with _double curly braces_ to display a component property
    * **ngFor** to display an array of items
    * A `Typescript` class to shape the **model data** for your component and display properties of that model
    * **ngIf** to conditionally display a chunk of `HTML` based on a `boolean` expression

Here is the final code:

`src/app/app.component.ts`: 
```typescript
import { Component } from '@angular/core';

import { Hero } from './hero';

@Component({
  selector: 'app-root',
  template: `
  <h1>{{title}}</h1>
  <h2>My favorite hero is: {{myHero.name}}</h2>
  <p>Heroes:</p>
  <ul>
    <li *ngFor="let hero of heroes">
      {{ hero.name }}
      </li>
  </ul>
  <p *ngIf="heroes.length > 3">There are many heroes!</p>
`
})
export class AppComponent {
  title = 'Tour of Heroes';
  heroes = [
    new Hero(1, 'Windstorm'),
    new Hero(13, 'Bombasto'),
    new Hero(15, 'Magneta'),
    new Hero(20, 'Tornado')
  ];
  myHero = this.heroes[0];
}
```

`src/app/hero.ts`:
```typescript
export class Hero {
  constructor(
    public id: number,
    public name: string) { }
}
```

`src/app/app.module.ts`:
```typescript
import { NgModule } from '@angular/core';
import { BrowserModule }  from '@angular/platform-browser';

import { AppComponent } from './app.component';

@NgModule({
  imports: [
    BrowserModule
  ],
  declarations: [
    AppComponent
  ],
  bootstrap: [ AppComponent ]
})
export class AppModule { }
```

`main.ts`:
```typescript
import { enableProdMode } from '@angular/core';
import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';

import { AppModule } from './app/app.module';
import { environment } from './environments/environment';

if (environment.production) {
  enableProdMode();
}

platformBrowserDynamic().bootstrapModule(AppModule);
```

---

[Angular Docs](https://angular.io/guide/displaying-data)