##### 5/07/2020
# Observable Overview - Defining Observers
A handler for receiving observable notifications implements the `Observer` interface.  It is an `object` that defines callback methods to handle the three types of notifications that an `observable`  can send:

| Notification Type | Required | Description |
|---|---|---|
| `next` | `true` | A handler for each delivered value.  Called zero or more times after execution starts. |
| `error` | `false` | A handler for an error notification.  An error halts execution of the `observable` instance. |
| `complete` | `false` | A handler for the execution-complete notification.  Delayed values can continue to be delivered to the next handler after execution is complete. |

An observer `object` can define any combination of these handlers.  If you don't supply a handler for a notification type, the `observer` ignores notifications of that type.

---

[Angular Docs](https://angular.io/guide/observables#defining-observers)