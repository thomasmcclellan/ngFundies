##### 2/25/2020
# Pipes - Power Boost Calculator
It's not much fun updating the template to test the custom pipe.  Upgrade the example to a "Power Boost Calculator" that combines your pipe and two-way data binding with `ngModel`.

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-power-boost-calculator',
  template: `
    <h2>Power Boost Calculator</h2>
    <div>Normal power: <input [(ngModel)]="power"></div>
    <div>Normal factor: <input [(ngModel)]="factor"></div>
    <p>Super Hero Power: {{ power | exponentialStrength: factor }}</p>
  `
})
export class PowerBoostCalculatorComponent {
  power: number = 5;
  factor: number = 1;
}
```

![Power Boost Calculator](../../../Assets/powerBoostCalculatorDemo.gif)
  
---

[Angular Docs](https://angular.io/guide/pipes#power-boost-calculator)