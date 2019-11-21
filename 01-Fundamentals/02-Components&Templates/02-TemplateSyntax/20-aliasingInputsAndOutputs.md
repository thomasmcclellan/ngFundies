##### 11/20/2019
# Template Syntax - Aliasing `inputs` and `outputs`
Sometimes the public name of an `input`/`output` property should be different from the internal name.  While it is a best practice to avoid this situation, `Angular` _does_ offer a solution.

## Aliasing in the Metadata:
Alias `inputs` and `outputs` in the metadata using a colon-delimited (`:`) `string` with the directive property name on the left and the public alias on the right:

```typescript
inputs: ['input1: saveForLaterItem'], // propertyName: alias
outputs: ['outputEvent1: saveForLaterEvent']
```

## Aliasing with the `@Input()`/`@Output()` Decorator:
You can specify the alias for the property name by passing the alias name to the `@Input()`/`@Output()` decorator.  The internal name remains as usual.

```typescript
@Input('wishListItem') input2: string // @Input(alias)
@Output('wishEvent') outputEvent2: new EventEmitter<string>() // @Output(alias) propertyName = ...
```

---

[Angular Docs](https://angular.io/guide/template-syntax#aliasing-inputs-and-outputs)