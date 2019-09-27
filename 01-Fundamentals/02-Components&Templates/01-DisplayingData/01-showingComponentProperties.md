##### 9/23/2019
# Introduction to Displaying Data - Showing Component Properties with Interpolation
The easiest way to display a component property is to bind the property name through **interpolation**.  With interpolation, you put the property name in the view template, enclosed in double curly braces: `{{ myHero }}`.

`src/app/app.component.ts`: 
```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <h1>{{ title }}</h1>
    <h2>My favorite hero is: {{ myHero }}</h2>
  `
})
export class AppComponent {
  title = 'Tour of Heroes'
  myHero = 'Windstorm'
}
```

`Angular` automatically pulls the value of the `title` and `myHero` properties from the component and inserts those values into the browser.  `Angular` updates the display when these properties changes.

  > More precisely, the redisplay occurs after some kind of asynchronous event related to the view, such as a keystroke, a time completion, or a response to an HTTP request.

---

[Angular Docs](https://angular.io/guide/displaying-data)