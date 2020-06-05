##### 6/03/2020
# Launching Apps with a Root Module - The `declarations` `Array`
The module's `declarations` `array` tells `Angular` which components belong to that module. As you create more components, add them to declarations.

You must declare every component in exactly one `NgModule` `class`. If you use a component without declaring it, `Angular` returns an error message.

The `declarations` `array` only takes _declarables_. Declarables are components, directives and pipes. All of a module's declarables must be in the `declarations` `array`. Declarables must belong to exactly one module. The compiler emits an error if you try to declare the same `class` in more than one module.

These declared `classes` are visible within the module but invisible to components in a different module unless they are exported from this module and the other module imports this one.

An example of what goes into a `declarations` `array` follows:

```ts
declarations: [
  YourComponent, 
  YourPipe,
  YourDirective
]
```

A declarable can only belong to one module, so ony declare it in one `@NgModule`.  When you need it elsewhere, import the module that has the declarable you need in it.

  > **NOTE**: **Only**  `@NgModule` **references** go in the `imports` `array`.

## Using Directives with `@NgModule`:
Use the `declarations` `array` for directives. To use a directive, component, or pipe in a module, you must do a few things:
  1. Export it from the file where you wrote it.
  2. Import it into the appropriate module.
  3. Declare it in the `@NgModule` declarations array.

Those three steps look like the following. In the file where you create your directive, export it. The following example, named `ItemDirective` is the default directive structure that the CLI generates in its own file, `item.directive.ts`:

```ts
import { Directive } from '@angular/core';

@Directive({
  selector: '[appItem]'
})
export class ItemDirective {
// code goes here
  constructor() { }

}
```

The key point here is that you have to export it so you can import it elsewhere. Next, import it into the `NgModule`, in this example `app.module.ts`, with a `JS` import statement:

```ts
import { ItemDirective } from './item.directive';
```

And in the same file, add it to the `@NgModule` `declarations` array:

```ts
declarations: [
  AppComponent,
  ItemDirective
]
```

Now you could use your `ItemDirective` in a component. This example uses `AppModule`, but you'd do it the same way for a feature module. 

  > **Remember**:  Components, directives, and pipes belong to one module only. You only need to declare them once in your app because you share them by importing the necessary modules. This saves you time and helps keep your app lean.

---

[Angular Docs](https://angular.io/guide/bootstrapping#the-declarations-array)