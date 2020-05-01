##### 5/01/2020
# Dynamic Forms - Questionnaire Data
`DynamicFormComponent` expects the list of questions in the form of an `array` bound to `@Input()` `questions`.

The set of questions you've defined for the job application is returned from the `QuestionService`.  In a real app you'd retrieve these questions from storage.

The key point is that you control the hero job application questions entirely through the `objects` returned from `QuestionService`.  Questionnaire maintenance is a simple matter of adding, updating, and removing `objects` from the `questions` `array`.

```ts
import { Injectable } from '@angular/core';
import { DropdownQuestion } from './question-dropdown';
import { QuestionBase } from './question-base';
import { TextboxQuestion } from './question-textbox';
import { of } from 'rxjs';

@Injectable()
export class QuestionService {
  // TODO: get from a remote source of question metadata
  getQuestions() {
    let questions: QuestionBase<string>[] = [
      new DropdownQuestion({
        key: 'brave',
        label: 'Bravery Rating',
        options: [
          { key: 'solid', value: 'Solid' },
          { key: 'great', value: 'Great' },
          { key: 'good', value: 'Good' },
          { key: 'unproven', value: 'Unproven' }
        ],
        order: 3
      }),
      
      new TextboxQuestion({
        key: 'firstName',
        label: 'First Name',
        value: 'Bombasto',
        required: true,
        order: 1
      }),

      new TextboxQuestion({
        key: 'emailAddress',
        label: 'Email',
        type: 'email',
        order: 2
      })
    ];

    return of(questions.sort((a, b) =>  a.order - b.order));
  }
}
```

Finally, display an instance of the form in the `AppComponent shell.

```ts
import { Component } from '@angular/core';
import { QuestionService } from './question-base';
import { QuestionBase } from './question-base';
import { Observable } from 'rxjs';

@Component({
  selector: 'app-root',
  template: `
    <div>
      <h2>Job Application for Heroes</h2>
      <app-dynamic-form [questions]="questions$ | async"></app-dynamic-form>
    </div>
  `,
  providers: [QuestionService]
})
export class AppComponent {
  questions$: Observable<QuestionBase<any>[]>;

  constructor(service: QuestionService) {
    this.questions$ = service.getQuestions();
  }
}
```

---

[Angular Docs](https://angular.io/guide/dynamic-form#questionnaire-data)