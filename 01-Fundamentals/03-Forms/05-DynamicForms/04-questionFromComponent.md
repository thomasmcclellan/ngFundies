##### 4/30/2020
# Dynamic Forms - Question Form Component
Now that you have defined the complete model you are ready to create components to represent the dynamic form.  

`DynamicFormComponent` is the entry point and the main container for the form.

```html
<!-- dynamic-form.component.html -->
<div>
  <form (ngSubmit)="onSubmit()" [formGroup]="form">
    <div *ngFor="let question of questions" class="form-row">
      <app-question [question]="question" [form]="form"></app-question>
    </div>

    <div class="form-row">
      <button type="submit" [disabled]="!form.valid">Save</button>
    </div>
  </form>

  <div *ngIf="payLoad" class="form-row">
    <strong>Saved the following values</strong>
    <br>
    {{payLoad}}
  </div>
</div>
```

```ts
// dynamic-form.component.ts
import { Component, Input, OnInit } from '@angular/core';
import { FormGroup } from '@angular/forms';
import { QuestionBase } from './question-base';
import { QuestionControlService } from './question-control.service';

@Component({
  selector: 'app-dynamic-form',
  templateUrl: './dynamic-form.component.html',
  providers: [ QuestionControlService ]
})
export class DynamicFormComponent implements OnInit {
  @Input() questions: QuestionBase<string>[] = [];
  form: FormGroup;
  payLoad = '';

  constructor(private qcs: QuestionControlService) { }

  ngOnInit() {
    this.form = this.qcs.toFormGroup(this.questions);
  }

  onSubmit() {
    this.payLoad = JSON.stringify(this.form.getRawValue());
  }
}
```

It presents a list of questions, each bound to a `<app-question>` component element.  The `<app-question>` tag matches the `DynamicFormQuestionComponent`, the component responsible for rendering the details of each _individual_ question based on values in the data-bound question `object`.

```html
<!-- dynamic-form-question.component.html -->
<div [formGroup]="form">
  <label [attr.for]="question.key">{{ question.label }}</label>
  <div [ngSwitch]="question.controlType">
    <input 
      *ngSwitchCase="'textbox'" 
      [formControlName]="question.key"
      [id]="question.key" 
      [type]="question.type"
    >

    <select 
      [id]="question.key" 
      *ngSwitchCase="'dropdown'" 
      [formControlName]="question.key"
    >
      <option 
        *ngFor="let opt of question.options" 
        [value]="opt.key"
      >{{ opt.value }}</option>
    </select>
  </div>

  <div class="errorMessage" *ngIf="!isValid">{{ question.label }} is required</div>
</div>
```

```ts
// dynamic-form-question.component.ts
import { Component, Input } from '@angular/core';
import { FormGroup } from '@angular/form';
import { QuestionBase } from './question-base';

@Component({
  selector: 'app-question',
  templateUrl: './dynamic-form-question.component.html'
})
export class DynamicFormQuestionComponent {
  @Input() question: QuestionBase<string>;
  @Input() form: FormGroup;

  get isValid() {
    return this.form.controls[this.question.key].valid;
  }
}
```

Notice this component can present any type of question in your model.  You only have two types of questions at this point but you can imagine many more.  The `ngSwitch` determines which type of question to display.

In both components you're relying on `Angular`'s **formGroup** to connect the template `HTML` to the underlying control `objects` populated from the question model with display and validation rules.  

`formControlName` and `formGroup` are directives defined in `ReactiveFormsModule`. The templates can access these directives directly since you imported `ReactiveFormsModule` from `AppModule`.

---

[Angular Docs](https://angular.io/guide/dynamic-form#question-form-components)