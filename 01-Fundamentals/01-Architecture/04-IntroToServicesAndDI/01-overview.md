##### 9/18/2019
# Introduction to Services and Dependency Injection - Overview
**Service** is a broad category encompassing any value, function, or feature that an app needs.  A service is typically a class with a narrow, well-defined purpose.  It should do something specific and do it well.

`Angular` distinguishes components from services to increase modularity and reusability.  By separating a component's view-related functionality from other kinds of processing, you can make you component classes lean and efficient.

Ideally, a component's job is to enable the user experience adn nothing more.  A component should present properties and methods for data binding, in order to mediate between the view (rendered by the template) and the application logic (which often includes some notion of a **model**).

A component can delegate certain tasks to services, such as fetching data from the server, validating user input, or logging directly to the console.  By defining such processing tasks in an _injectable service class_, ou make those tasks available to any component.  You can also make your app more adaptable by injecting different providers of the same kind of service, as appropriate in different circumstances.

  > `Angular` does not _enforce_ these principles; it does, however, help you _follow_ these principles by making it easy to factor you application logic into services and make those services available to components through **dependency injection**.

---

[Angular Docs](https://angular.io/guide/architecture-services)