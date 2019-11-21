##### 11/19/2019
# Template Syntax - `@Input()` and `@Output()` Declarations
Instead of using the `@Input()` and `@Output()` decorators to declare inputs and outputs, you can identify members in the `inputs` and `outputs` `arrays` of the directive metadata, as in this example:

```typescript
inputs: ['clearanceItem'],
outputs: ['buyEvent']
```

While declaring `inputs` and `outputs` in the `@Directive` and `@Component` metadata is possible, it is a better practice to use the `@Input()` and `@Output()` class decorators instead, as follows:

```typescript
@Input() item: string
@Output() deleteRequest = new EventEmitter<string>()
```

  > See [Decorate Input and Output Properties](https://angular.io/guide/styleguide#decorate-input-and-output-properties) for details.

  > If you get a template parse error when trying to use inputs or outputs, buy you know that the properties do indeed exist, double check that your properties are annotated with `@Input()`/`@Output()` or that you've declared them in an `inputs`/`outputs` `array`:
  >
  > ```
  > Uncaught Error: Template parse errors:
  > Can't bind to 'item' since it isn't a known property of 'app-item-detail'
  > ```

---

[Angular Docs](https://angular.io/guide/template-syntax#input-and-output-declarations)