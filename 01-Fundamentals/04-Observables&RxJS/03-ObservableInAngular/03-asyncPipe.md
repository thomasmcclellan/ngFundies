##### 5/18/2020
# `Observables` in `Angular` - Async Pipe
The [AsyncPipe](https://angular.io/api/common/AsyncPipe) subscribes to an `observable` or `promise` and returns the latest value it has emitted.  When a new value is emitted, the pipe marks the component to be checked for changes.

The following example binds the `time` `observable` to the component's view.  The `observable` continuously updates the view with the current time.

```ts
@Component({
  selector: 'async-observable-pipe',
  template: `
    <div>
      <code>observable | async</code>: 
      Time: {{ time | async }}
    </div>
  `
})
export class AsyncObservablePipeComponent {
  time = new Observable<string>(observer => 
    setInterval(() => observer.next(new Date().toString()), 1000);
  );
}
```

---

[Angular Docs](https://angular.io/guide/observables-in-angular#async-pipe)