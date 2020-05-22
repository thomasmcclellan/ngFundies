##### 5/19/2020
# `Observables` in `Angular` - Router
`Router.events` provides events as `observables`.  You can use the `filter()` operator from `RxJS` to look for events of interest, and subscribe to them in order to make decisions based on the sequence of the event int the navigation process.  Here's an example:

```ts
import { Router, NavigationStart } from '@angular/core';
import { filter } from 'rxjs/operators';

@Component({
  selector: 'app-routable',
  templateUrl: './routable.component.html',
  styleUrls: ['./routable/component.css']
})
export class Routable1Component implements OnInit {
  navStart: Observable<NavigationStart>;

  constructor(private router: Router) {
    // Create a new Observable that publishes only the NavigationStart event
    this.navStart = router.events.pipe(
      filter(evt => even instanceof NavigationStart)
    ) as Observable<NavigationStart>;
  }

  ngOnInit() {
    this.navStart.subscribe(evt => console.log('Navigation Started'));
  }
}
```

The [ActivatedRoute](https://angular.io/api/router/ActivatedRoute) is an injected router service that makes use a `observables` to get information about a route path and parameter.  For example, `ActivatedRoute.url` contains an `observable` that reports the route path or paths.  Here's an example:

```ts
import { ActivatedRoute } from '@angular/core';

@Component({
  selector: 'app-routable',
  templateUrl: './routable.component.html',
  styleUrls: ['./routable.component.css']
})
export class Routable2Component implements OnInit {
  constructor(private activatedRoute: ActivatedRoute) { }

  ngOnInit() {
    this.activatedRoute.url
      .subscribe(url => console.log(`The URL changed to: ${url}`));
  }
}
```

---

[Angular Docs](https://angular.io/guide/observables-in-angular#router)