##### 9/19/2019
# Introduction to Services and Dependency Injection - Service Example
Here's an example of a service class that logs to the browser console:

`src/app/logger.service.ts` (class):
```js
export class Logger {
  log(msg: any) { console.log(msg) }
  error(msg: any) { console.log(msg) }
  warn(msg: any) { console.log(msg) }
}
```

**Services** can depend on other services.  For example, here's a `HeroService` that depends on the `Logger` service, and also use `BackendService` to get heroes.  That service in turn might depend on the `HttpClient` service to fetch heroes asynchronously from a server.

`src/app/hero.service.ts` (class):
```js
export class HeroService {
  private heroes: Hero[] = []

  constructor(
    private backend: BackendService,
    private logger: Logger) { }

  getHeroes() {
    this.backend.getAll(Hero).then( (heroes: Hero[]) => {
      this.logger.log(`Fetched ${heroes.length} heroes.`)
      this.heroes.push(...heroes) // fill cache
    });
    return this.heroes
  }
}
```

---

[Angular Docs](https://angular.io/guide/architecture-services)