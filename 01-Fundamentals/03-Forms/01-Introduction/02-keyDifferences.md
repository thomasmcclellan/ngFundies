##### 3/02/2020
# Forms Introduction - Key Differences
The table below summarizes the key differences between reactive and template-driven forms.

|| Reactive | Template-Driven |
|---|---|---|
| Setup (form model) | More explicit, created in component class | Less explicit, created by directives |
| Data model | Structural | Unstructured |
| Predictability | Synchronous | Asynchronous |
| Form validation | Functions | Directives |
| Mutability | Immutable | Mutable |
| Scalability | Low-level API access | Abstraction on top of APIs |

## Common Foundation:
Both reactive and template-driven forms share underlying building blocks.
  * `FormControl` tracks the value and validation status of an individual form control
  * `FormGroup` tracks the same values and status for a collection of form controls
  * `FormArray` tracks tha same values and status for an `array` of form controls
  * `ControlValueAccessor` creates a bridge between `Angular` `FormControl` instances and native `DOM` elements
  
---

[Angular Docs](https://angular.io/guide/forms-overview#key-differences)