##### 4/29/2020
# Dynamic Forms - Question Model
The next step is to define an `object` model that can describe all scenarios needed by the form functionality.  The hero application process involves a form with a lot of questions.  The _question_ is the most fundamental `object` in the model.

The following `QuestionBase` is a fundamental question `class`.

```ts
export class QuestionBase<T> {
  value: T;
  key: string;
  label: string;
  required: boolean;
  order: number;
  controlType: string;
  type: string;
  questions: { key: string, value: string }[];

  constructor(options: {
    value?: T;
    key?: string;
    label?: string;
    required?: boolean;
    order?: number;
    controlType?: string;
    type?: string;
  } = { }) {
    this.value = options.value;
    this.key = options.key || '';
    this.label = options.label || '';
    this.required = !!options.required;
    this.order = options.order === undefined ? 1 : options.order;
    this.controlType = options.controlType || '';
    this.type = options.type || '';
  }
}
```

From this base you can derive two new classes in `TextboxQuestion` and `DropdownQuestion` that represent textbox and dropdown questions.  The idea is that the form will be bound to specific question types and render the appropriate controls dynamically.

`TextboxQuestion` supports multiple `HTML5` types such as text, email, and url via the type property.

```ts
import { QuestionBase } from './question-base';

export class TextboxQuestion extends QuestionBase<string> {
  controlType = 'textbox';
  type: string;

  constructor(options: {} = {}) { 
    super(options);
    this.type = options['type'] || '';
  }
}
```

`DropdownQuestion` presents a list of choices in a select box.

```ts
import { QuestionBase } from './question-base';

export class DropdownQuestion extends QuestionBase<string> {
  controlType = 'dropdown';
  options: { key: string, value: string }[] = [];

  constructor(options: {} = {}) {
    super(options);
    this.options = options['options'] || [];
  }
}
```

Next is `QuestionControlService`, a simple service for transforming the questions to the `FormGroup`.  In a nutshell, the form group consumes the metadata from the question model and allows you to specify default values and validation rules.

```ts
import { Injectable } from '@angular/core';
import { FormControl, FormGroup, Validators } from '@angular/forms';

import { QuestionBase } from './question-base';

@Injectable()
export class QuestionControlService {
  constructor() { }

  toFormGroup(questions: QuestionBase<string>[]) {
    let group: any = {};

    questions.forEach(question => {
      group[question.type] = question.required 
        ? new FormControl(question.value || '', Validators.required) 
        : new FormControl(question.value || '');
    });

    return new FormGroup(group);
  }
}
```

---

[Angular Docs](https://angular.io/guide/dynamic-form#question-model)