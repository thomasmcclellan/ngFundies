##### 5/05/2020
# Observable Overview - Using Observables to Pass Values
`Observables` provides support for passing messages between parts of your application.  they are used frequently in `Angular` and are the recommended technique for event handling, asynchronous programming, and handling multiple values.

The observer pattern is a software design pattern in which an `object`, called the _subject_, maintains a list of its dependents, called _observers_, and notifies them automatically of state changes.  This pattern is similar (but not identical) to the [publish/subscribe]() design pattern.

`Observables` are declarative--that is, you define a `function` for publishing values, but it not executed until a consumer subscribes to it.  The subscribed consumer then receives notifications until the `function` completes, or until they unsubscribe.

An `observable` can deliver multiple values of any type--literal, messages, or events, depending on the context.  the API for receiving values in the same whether the values are delivered synchronously or asynchronously.  Because setup and teardown logic are both handled by the `observable`, your application code only needs to worry about subscribing to consume values, and when done, unsubscribing.  Whether the stream was keystrokes, an HTTP response, or an interval timer, the interface for listening to values and stopping listening is the same.

Because of these advantages, `observables` are used extensively within `Angular`, and are recommended for app development as well.

---

[Angular Docs](https://angular.io/guide/observables#using-observables-to-pass-values)