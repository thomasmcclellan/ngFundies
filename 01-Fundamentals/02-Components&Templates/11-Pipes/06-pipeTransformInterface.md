##### 2/24/2020
# Pipes - The PipeTransform Interface
  > **The _PipeTransform_ Interface**:
  >
  > The `transform` method is essential to a pipe.  The `PipeTransform` _interface_ defines that method and guides both tooling and the compiler.  Technically, it's optional; `Angular` looks for and executes the `transform` method regardless.

Now you need a component to demonstrate the pipe.

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-power-booster',
  template: `
    <h2>Power Booster</h2>
    <p> Super power boost: {{ 2 | exponentialStrength: 10 }}</p>
  `
})
export class PowerBoosterComponent { }
```

![Custom Pipe](../../../Assets/customPipe.png)

Note the following:
  * You use your custom pipe the same way you use built-in pipes
  * You must include your pipe in the `declarations` `array` of the `AppModule`
  * If you choose to inject your pipe into a class, you must provide it in the `providers` `array` of your `NgModule`

  > **REMEMBER THE DECLARATIONS ARRAY**:
  > 
  > You must register custom pipes.  If you don't, `Angular` reports an error.  The [`Angular` CLI's](https://angular.io/cli) generator registers the pipe automatically.

  > To probe the behavior in the [live example](https://stackblitz.com/angular/njnorvdmvvx?file=src%2Fapp%2Fapp.component.html), change the value and optional exponent in the template.
  
---

[Angular Docs](https://angular.io/guide/pipes#the-pipetransform-interface)