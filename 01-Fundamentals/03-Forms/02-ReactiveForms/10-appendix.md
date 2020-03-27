##### 3/23/2020
# Reactive Forms - Appendix
## Reactive Form API:
Listed below are the base `classes` and services used to create and manage form controls.

### `Classes`:
| Class | Description |
|---|---|
| `AbstractControl` | The abstract base `class` for the concrete form control classes `FormControl`, `FormGroup`, and `FormArray`.  It provides their common behaviors and properties |
| `FormControl` | Manages the value and validity status of an individual form control.  It corresponds to an `HTML` form control such as `<input>` or `<select>` |
| `FormGroup` | Manages the value and validity state of a group of `AbstractControl` instances.  The group's properties include its child controls.  The top-level form in your component is `FormGroup` |
| `FormArray` | Manages the value and validity state of a numerically indexed `array` of `AbstractControl` instances |

## Directives:
| Directive | Description |
|---|---|
| `FormControlDirective` | Syncs a standalone `FormControl` instance to a form control element |
| `FormControlName` | Syncs `FormControl` in an existing `FormGroup` instance to a form control element by name |
| `FormGroupDirective` | Syncs an existing `FormGroup` instance to a `DOM` element |
| `FormGroupName` | Syncs a nested `FormGroup` instance to a `DOM` element |
| `FormArrayName` | Syncs a standalone `FormArray` instance to a `DOM` element |

---

[Angular Docs](https://angular.io/guide/reactive-forms#appendix)