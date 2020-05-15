##### 5/15/2020
# `Observables` in `Angular` - HTTP
`Angular`'s `HttpClient` returns `observables` from HTTP method calls. For instance, `http.get('/api')` returns an `observable`.  This provides several advantages over promise-based HTTP APIs:
  * `Observables` do not mutate the server response (as can occur through chained `.then()` calls on promises).  Instead, you can use a series of operators to transform values as needed
  * HTTP requests are cancellable through the `unsubscribe()` method
  * Requests can be configured to get process event updates
  * Failed requests can be retried easily

---

[Angular Docs](https://angular.io/guide/observables-in-angular#http)