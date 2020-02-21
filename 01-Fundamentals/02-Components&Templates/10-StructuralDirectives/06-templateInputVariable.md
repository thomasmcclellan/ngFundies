##### 2/12/2020
# Structural Directives - Template Input Variable
A _template input variable_ is a variable whose value you can reference _within_ a single instance of the template. There are several such variables in this example: `hero`, `i`, and `odd`.  All are preceded by the keyword `let`.

A _template input variable_ is _**not**_ the same as a _template reference variable_, either _semantically_, nor _syntactically_.

You declare a template _input_ variable using the `let` keyword (`let hero`).  The variable's scope is limited to a single instance of the repeated template.  You can use the same variable name again in the definition of other structural directives.

You declare a template _reference_ variable by prefixing the variable name with `#` (`#var`).  A reference variable refers to its attached element, component, or directive.  It can be accessed anywhere in the entire template.

Template input and reference variable names have their own namespace.  The `hero` in `let hero` is never the same variable as the `hero` declared as `#hero`.

---

[Angular Docs](https://angular.io/guide/structural-directives#template-input-variable)