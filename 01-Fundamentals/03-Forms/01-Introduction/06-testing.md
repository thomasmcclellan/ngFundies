##### 3/06/2020
# Forms Introduction - Testing
Testing plays a large part in complex applications and a simpler testing strategy is useful when validating that your forms function correctly.  Reactive forms and template-driven forms have different levels of reliance on rendering the UI to perform assertions based on form control and form field changes.  The following examples demonstrate the process of testing forms with reactive and template-driven forms.

## Testing Reactive Forms:
Reactive forms provide a relatively easy testing strategy because they provide synchronous access to the form and data models, and they can be tested without rendering the UI.  In these tests, status and data are queried and manipulated through the control without interacting with the change detection cycle.

The following tests use the favorite color components mentioned earlier to verify the data flows from view to model and model to view for a reactive form.

The following test verifies the data flow from view to model.

```ts
it('should update the value of the input field', () => {
  const input = fixture.nativeElement.querySelector('input'),
        event = createNewEvent('input');

  input.value = 'Red';
  input.dispatchEvent(event);

  expect(fixture.componentInstance.favoriteColorControl.value).toEqual('Red');
});
```

Here are the steps performed in the view to model test.
  1. Query the view for the form input element, and create a custom 'input' event for the test
  2. Set the new value for the input to _Red_, adn dispatch the 'input' event on the form input element
  3. Assert that the component's `favoriteColorControl` value matches the value from the input

The following test verifies the data flow from model to view.

```ts
it('should update the value in the control', () => {
  component.favoriteColorControl.setValue('Blue');

  const input = fixture.nativeElement.querySelector('input');

  expect(input.value).toBe('Blue');
});
```

Here are the steps performed in the model to view test:
  1. Use the `favoriteColorControl`, a `FormControl` instance, to set the new value
  2. Query the view for the form input element
  3. Assert that the new value set on the control matches the value in the input

## Testing Template-Driven Forms:
Writing tests with template-driven forms requires a detailed knowledge of the change detection process and an understanding of how directives run on each cycle to ensure that elements are queried, tested, or changed at the correct time.

The following tests use the favorite color components mentioned earlier to verify the data flows from view to model and model to view for a template-driven form.

The following test verifies the data flow from view to model.

```ts
it('should update the favorite color in the component', () => {
  const input = fixture.nativeElement.querySelector('input'),
        event = createNewEvent('input');

  input.value = 'Red';
  input.dispatchEvent(event);

  fixture.detectChanges();

  expect(component.favoriteColor).toEqual('Red');
});
```

Here are the steps performed in the view model test:
  1. Query the view for the form input element, and create a custom 'input' event for the test
  2. Set the new value for the input to _Red_, and dispatch the 'input' event on the form input element
  3. Run change detection through the test fixture
  4. Assert that the component `favoriteColor` property value matches the value from the input

The following test verifies the data flow from model to view.

```ts
it('should update the favorite color on the input field', () => {
  component.favoriteColor = 'Blue';

  fixture.detectChanges();

  tick();

  const input = fixture.nativeElement.querySelector('input');

  expect(input.value).toBe('Blue');
});
```

Here are the steps performed in the model to view test:
  1. Use the component instance to set the value fo the `favoriteColor` property
  2. Run change detection through the test fixture
  3. Use the `tick()` method to simulate the passage of time within the `fakeAsync)` task
  4. Query the view for the form input element
  5. Assert that the input value matches the value of the `favoriteColor` property in the component instance
  
---

[Angular Docs](https://angular.io/guide/forms-overview#testing)