##### 9/06/2019
# Architecture Overview - Components
Every `Angular` application has at least one component, the _root component_ that connects a component hierarchy with the page document object model (`DOM`).  Each component defines a class that contains application data and logic, and is associated with an `HTML` _template_ that defines a view to be displayed in a target environment.

The `@Component()` **decorator** identifies the class immediately below it as a component, and provides the template and related component-specific metadata.

  > **Decorators** are functions that modify `JS` classes.  `Angular` defines a number of decorators that attach specific kinds of metadata to classes, so that the system knows what those classes mean and how they should work.

---

## Templates, Directives, and Data Binding
A **template** combines `HTML` with `Angular` markup that can modify `HTML` elements before they are displayed.  Template **directives** provide program logic, and **binding markup** connects your application data to the DOM.  There are two types of data binding:

  * **Event Binding**: lets your app respond to user input in the target environment by updating your application data
  * **Property Binding**: lets you interpolate values that are computed from your application data into the `HTML`

Before a view is displayed, `Angular` evaluates the directives and resolves the binding syntax in the template to modify the `HTML` elements and the DOM, according to your program data and logic.  `Angular` supports _two-way data binding_, meaning that changes in the DOM, such as user choices, are also reflected in your program dat.

Your templates can use **pipes** to improve the user experience by transforming values for display.  For example, use pipes to display dates and currency values that are appropriate for a user's locale.  `Angular` provides predefined pipes for common transformations, and you can also define your own pipes.

---

[Angular Docs](https://angular.io/guide/architecture)