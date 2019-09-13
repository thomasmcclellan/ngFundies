##### 9/06/2019
# Architecture Overview - Services and Dependency Injection
For data or logic that isn't associated with a specific view, and that you want to share across components, you create a **service** class.  A service class definition is immediately preceded by the `@Injectable()` **decorator**.  The decorator provides the metadata that allows other providers to be _injected_ as dependencies into your class.

**Dependency Injection** (DI) lets you keep your component classes lean and efficient.  They don't fetch data from the server, validate user input, or log directly to the console; **they delegate such tasks to the services**.

---

## Routing
The `Angular` **Router** NgModule provides a service that lets your define a navigation path among the different application states and view hierarchies in your app.  It is modeled on the familiar browser navigation conventions:

  * Enter a URL in the address bar and the browser navigates to a corresponding page
  * Click links on the page and the browser navigates to a new page
  * Click the browser's back and forward buttons and the browser navigates backwards and forwards, respectively, through the history of pages you've seen

The router maps URL-like paths to views instead of pages.  When a user performs an action, such as clicking a link, that would load a new page in the browser, the router intercepts the browser's behavior, and shows/hides view hierarchies.

If the router determines that the current application state requires particular functionality, and the module that defines it hasn't been loaded, the router can _lazy-load_ the module on demand.

The router interprets a link URL according to your app's view navigation rules and data state.  You can navigate to new views when the user clicks a button or selects from a drop box, or in response to some other stimulus from any source.  The router logs activity in the browser's history, so the back/forward buttons work as well.

To define navigation rules, you associate _navigation paths_ with your components.  A path uses a URL-like syntax that integrates your program data, in much the same way that template syntax integrates your views with your program data.  You can then apply program logic to choose which views to show/hide, in response to user input and your own access rules.

---

[Angular Docs](https://angular.io/guide/architecture)