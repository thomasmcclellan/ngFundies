##### 2/24/2020
# Pipes - Custom Pipes
You can write your own custom pipes.  Here's a custom pipe named `ExponentialStrengthPipe` that can boost a hero's powers:

```ts
import { Pipe, PipeTransform } from '@angular/core';
/*
  * Raise the value exponentially
  * Takes an exponent argument that defaults to 1.
  * Usage:
  *   value | exponentialStrength: exponent
  * Example:
  *   {{ 2 | exponentialStrength: 10 }}
  *   formats to: 1024
*/
@Pipe({ name: 'exponentialStrength' })
export class ExponentialStrengthPipe implements PipeTransform {
  transform(value: number, exponent?: number) : number {
    return Math.pow(value, isNaN(exponent) ? 1 : exponent);
  }
}
```

This pipe definition reveals the following key points:
  * A pipe is a class decorated with pipe metadata
  * The pipe class implements the `PipeTransform` interface's `transform` method that accepts an input value followed by optional parameters and returns the transformed value
  * There will be one additional argument to the `transform` method for each parameter passed to the pipe.  Your pipe has one such parameter: the `exponent`
  * To tell `Angular` that this is a pipe, you apply the `@Pipe` decorator, which you import from the `core` `Angular` library
  * The `@Pipe` decorator allows you to define the pipe name that you'll use within template expressions.  It must be a valid `JS` identifier.  Your pipe's name is `exponentialStrength`

---

[Angular Docs](https://angular.io/guide/pipes#custom-pipes)