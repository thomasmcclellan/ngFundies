##### 2/21/2020
# Structural Directives - Summary
  > You can try this guide in the [live example](https://stackblitz.com/angular/njpxvalbpgg?file=src%2Fapp%2Fapp.component.ts).

This is the source from the `src/app` folder:

```ts
// app.component.ts
import { Component } from '@angular/core';
import { Hero, heroes } from './hero';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: './app.component.css'
})
export class AppComponent {
  heroes = heroes;
  hero = this.heroes[0];
  condition: boolean = false;
  logs: string[] = [];
  showSad: boolean = true;
  status: string = 'ready';

  trackById(index: number, hero: Hero) : number { return hero.id; }
}
```

```html
<!-- app.component.html -->
<h1>Structural Directives</h1>
<p>Conditional display of hero</p>
<blockquote>
  <div 
    *ngIf="hero" 
    class="name"
  >{{ hero.name }}</div>
</blockquote>
<p>List of heroes</p>
<ul>
  <li *ngFor="let hero of heroes">{{ hero.name }}</li>
</ul>

<hr>

<h2 id="ngIf">NgIf</h2>
<p *ngIf="true">Expression is true and ngIf is true. This paragraph is in the DOM.</p>
<p *ngIf="false">Expression is false and ngIf is false. This paragraph is not in the DOM.</p>
<p [style.display]="'block'">Expression sets display to "block". This paragraph is visible.</p>
<p [style.display]="'none'">Expression sets display to "none". This paragraph is hidden but still in the DOM.</p>

<h4>NgIf with template</h4>
<p>&lt;ng-template&gt; element</p>
<ng-template [ngIf]="hero">
  <div class="name">{{ hero.name }}</div>
</ng-template>

<hr>

<h2 id="ng-container">&lt;ng-container&gt;</h2>
<h4>*ngIf with a &lt;ng-container&gt;</h4>
<button (click)="hero = hero ? null : heroes[0]">Toggle hero</button>
<p>
  I turned the corner
  <ng-container *ngIf="hero">
    and saw {{ hero.name }}. I waved
  </ng-container>
  and continued on my way.
</p>
<p>
  I turned the corner
  <span *ngIf="hero">
    and saw {{ hero.name }}. I waved
  </span>
  and continued on my way.
</p>

<p><i>&lt;select&gt; with &lt;span&gt;</i></p>
<div>
  Pick your favorite hero (
    <label>
      <input 
        type="checkbox" 
        checked 
        (change)="showSad = !showSad"
      >show sad
    </label>
  )
</div>
<select [(ngModel)]="hero">
  <span *ngFor="let hero of heroes">
    <span *ngIf="showSad || hero.emotion !== 'sad'">
      <option [ngValue]="hero">{{ hero.name }} ({{ hero.emotion }})</option>
    </span>
  </span>
</select>

<p><i>&lt;select&gt; with &lt;ng-container&gt;</i></p>
<div>
  Pick your favorite hero (
    <label>
      <input 
        type="checkbox" 
        checked 
        (change)="showSad = !showSad"
      >show sad
    </label>
  )
</div>
<select [(ngModel)]="hero">
  <ng-container *ngFor="let hero of heroes">
    <ng-container *ngIf="showSad || hero.emotion !== 'sad'">
      <option [ngValue]="hero">{{ hero.name }} ({{ hero.emotion }})</option>
    </ng-container>
  </ng-container>
</select>
<br><br>

<hr>

<h2 id="ngFor">NgFor</h2>
<div class="box">
<p class="code">&lt;div *ngFor="let hero of heroes; let i=index; let odd=odd; trackBy: trackById" [class.odd]="odd"&gt;</p>
<div *ngFor="let hero of heroes; let i=index; let odd=odd; trackBy: trackById" [class.odd]="odd">
  ({{i}}) {{hero.name}}
</div>

<p class="code">&lt;ng-template ngFor let-hero [ngForOf]="heroes" let-i="index" let-odd="odd" [ngForTrackBy]="trackById"/&gt;</p>
<ng-template ngFor let-hero [ngForOf]="heroes" let-i="index" let-odd="odd" [ngForTrackBy]="trackById">
  <div [class.odd]="odd">({{i}}) {{hero.name}}</div>
</ng-template>

</div>
<hr>

<h2 id="ngSwitch">NgSwitch</h2>

<div>Pick your favorite hero</div>
<p>
  <label *ngFor="let h of heroes">
    <input type="radio" name="heroes" [(ngModel)]="hero" [value]="h">{{h.name}}
  </label>
  <label><input type="radio" name="heroes" (click)="hero = null">None of the above</label>
</p>

<h4>NgSwitch</h4>

<div [ngSwitch]="hero?.emotion">
  <app-happy-hero    *ngSwitchCase="'happy'"    [hero]="hero"></app-happy-hero>
  <app-sad-hero      *ngSwitchCase="'sad'"      [hero]="hero"></app-sad-hero>
  <app-confused-hero *ngSwitchCase="'confused'" [hero]="hero"></app-confused-hero>
  <app-unknown-hero  *ngSwitchDefault           [hero]="hero"></app-unknown-hero>
</div>

<h4>NgSwitch with &lt;ng-template&gt;</h4>
<div [ngSwitch]="hero?.emotion">
  <ng-template [ngSwitchCase]="'happy'">
    <app-happy-hero [hero]="hero"></app-happy-hero>
  </ng-template>
  <ng-template [ngSwitchCase]="'sad'">
    <app-sad-hero [hero]="hero"></app-sad-hero>
  </ng-template>
  <ng-template [ngSwitchCase]="'confused'">
    <app-confused-hero [hero]="hero"></app-confused-hero>
  </ng-template >
  <ng-template ngSwitchDefault>
    <app-unknown-hero [hero]="hero"></app-unknown-hero>
  </ng-template>
</div>

<hr>

<h2>&lt;ng-template&gt;</h2>
<p>Hip!</p>
<ng-template>
  <p>Hip!</p>
</ng-template>
<p>Hooray!</p>

<hr>

<h2 id="appUnless">UnlessDirective</h2>
<p>
  The condition is currently
  <span [ngClass]="{ 'a': !condition, 'b': condition, 'unless': true }">{{condition}}</span>.
  <button
    (click)="condition = !condition"
    [ngClass] = "{ 'a': condition, 'b': !condition }" >
    Toggle condition to {{condition ? 'false' : 'true'}}
  </button>
</p>
<p *appUnless="condition" class="unless a">
  (A) This paragraph is displayed because the condition is false.
</p>

<p *appUnless="!condition" class="unless b">
  (B) Although the condition is true,
  this paragraph is displayed because appUnless is set to false.
</p>


<h4>UnlessDirective with template</h4>

<p *appUnless="condition">Show this sentence unless the condition is true.</p>

<p *appUnless="condition" class="code unless">
  (A) &lt;p *appUnless="condition" class="code unless"&gt;
</p>

<ng-template [appUnless]="condition">
  <p class="code unless">
    (A) &lt;ng-template [appUnless]="condition"&gt;
  </p>
</ng-template>
```

```css
/* app.component.css */
button {
  min-width: 100px;
  font-size: 100%;
}

.box {
  border: 1px solid gray;
  max-width: 600px;
  padding: 4px;
}
.choices {
  font-style: italic;
}

code, .code {
  background-color: #eee;
  color: black;
  font-family: Courier, sans-serif;
  font-size: 85%;
}

div.code {
  width: 400px;
}

.heroic {
  font-size: 150%;
  font-weight: bold;
}

hr {
  margin: 40px 0
}

.odd {
  background-color:  palegoldenrod;
}

td, th {
  text-align: left;
  vertical-align: top;
}

p span { color: red; font-size: 70%; }

.unless {
  border: 2px solid;
  padding: 6px;
}

p.unless {
  width: 500px;
}

button.a, span.a, .unless.a {
  color: red;
  border-color: gold;
  background-color: yellow;
  font-size: 100%;
}

button.b, span.b, .unless.b {
  color: black;
  border-color: green;
  background-color: lightgreen;
  font-size: 100%;
}
```

```ts
// app.module.ts
import { NgModule }      from '@angular/core';
import { FormsModule }   from '@angular/forms';
import { BrowserModule } from '@angular/platform-browser';

import { AppComponent }         from './app.component';
import { heroSwitchComponents } from './hero-switch.components';
import { UnlessDirective }    from './unless.directive';

@NgModule({
  imports: [ BrowserModule, FormsModule ],
  declarations: [
    AppComponent,
    heroSwitchComponents,
    UnlessDirective
  ],
  bootstrap: [ AppComponent ]
})
export class AppModule { }
```

```ts
// hero.ts
export interface Hero {
  id: number;
  name: string;
  emotion?: string;
}

export const heroes: Hero[] = [
  { id: 1, name: 'Dr. Nice', emotion: 'happy' },
  { id: 2, name: 'Narco', emotion: 'sad' },
  { id: 3, name: 'Windstorm', emotion: 'confused' },
  { id: 4, name: 'Magneta' }
];
```

```ts
// hero-switch.components.ts
import { Component, Input } from '@angular/core';
import { Hero } from './hero';

@Component({
  selector: 'app-happy-hero',
  template: `Wow. You like {{ hero.name }}.  What a happy hero...just like you.`
})
export class HappyHeroComponent {
  @Input() hero: Hero;
}

@Component({
  selector: 'app-sad-hero',
  template: `You like {{ hero.name }}? Such a sad hero. Are you sad too?`
})
export class SadHeroComponent {
  @Input() hero: Hero;
}

@Component({
  selector: 'app-confused-hero',
  template: `Are you as confused as {{ hero.name }}?`
})
export class ConfusedHeroComponent {
  @Input() hero: Hero;
}

@Component({
  selector: 'app-unknown-hero',
  template: `{{ message }}`
})
export class UnknownHeroComponent {
  @Input() hero: Hero;
  get message() {
    return this.hero && this.hero.name ?
      `${this.hero.name} is strange and mysterious.` :
      'Are you feeling indecisive?';
  }
}
```

```ts
// unless.directive.ts
import { Directive, Input, TemplateRef, ViewContainerRef } from '@angular/core';

@Directive({ selector: '[appUnless]'})
export class UnlessDirective {
  private hasView = false;

  constructor(
    private templateRef: TemplateRef<any>,
    private viewContainer: ViewContainerRef) { }

  @Input() set appUnless(condition: boolean) {
    if (!condition && !this.hasView) {
      this.viewContainer.createEmbeddedView(this.templateRef);
      this.hasView = true;
    } else if (condition && this.hasView) {
      this.viewContainer.clear();
      this.hasView = false;
    }
  }
}
```

---

[Angular Docs](https://angular.io/guide/structural-directives#summary)