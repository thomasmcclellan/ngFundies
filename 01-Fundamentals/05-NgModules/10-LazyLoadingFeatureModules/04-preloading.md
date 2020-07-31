##### 7/22/2020
# Lazy Loading Feature Modules - Preloading
Preloading improves UX by loading parts of your app in the background. You can preload modules or component data.

## Preloading Modules:
Preloading modules improves UX by loading parts of your app in the background so users don't have to wait for the elements to download when they activate a route.

To enable preloading of all lazy loaded modules, import the `PreloadAllModules` token from the `Angular` `router`.

```ts
import { PreloadAllModules } from '@angular/router';
```

Still in the `AppRoutingModule`, specify your preloading strategy in `forRoot()`.

```ts
RouterModule.forRoot(
  appRoutes,
  {
    preloadingStrategy: PreloadAllModules
  }
)
```

## Preloading Component Data:
To preload component data, you can use a `resolver`. Resolvers improve UX by blocking the page load until all necessary data is available to fully display the page.

### Resolvers:
Create a resolver service.  With the CLI, the command to generate a service is as follows:

```
ng generate service  
```

or

```
ng g s
```

In your service, import the following router members, implement `Resolve`, and inject the `Router` service.

```ts
import { Resolve } from '@angular/router';

...

export class CrisisDetailResolverService implements Resolve<> {
  resolve(
    route: ActivatedRouteSnapshot, 
    state: RouterStateSnapshot
  ) : Observable<> {
    ...
  }
}
```

Import this resolver into your module's routing module.

```ts
import { YourResolverService } from './your-resolver.service';
```

Add a `resolve` object to the component's `route` configuration.

```ts
{
  path: '/your-path',
  component: YourComponent,
  resolve: {
    crisis: YourResolverService
  }
}
```

In the component, use an `Observable` to get the data from the `ActivatedRoute`.

```ts
ngOnInit() {
  this.route.data
    .subscribe(param => {
      ...
    })
}
```

---

[Angular Docs](https://angular.io/guide/lazy-loading-ngmodules#preloading)