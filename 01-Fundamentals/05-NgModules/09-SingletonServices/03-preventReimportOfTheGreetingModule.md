##### 7/15/2020
# Singleton Services - Prevent Reimport of the `GreetingModule`
Only the root `AppModule` should import the `GreetingModule`.  If a lazy-loaded module imports it too, the app can generate multiple instances of a service.

To guard against a lazy loaded module re-importing `GreetingModule`, add the following `GreetingModule` constructor.

```ts
constructor(@Optional() @SkipSelf() parentModule?: GreetingModule) {
  if (parentModule) {
    throw new Error(
      'GreetingModule is already loaded.  Import it in the AppModule only';
    )
  }
}
```

The constructor tells `Angular` to inject the `GreetingModule` into itself.  The injection would be circular if `Angular` looked for `GreetingModule` in the _current_ injector, but the `@SkipSelf()` decorator means 'look for `GreetingModule` in an ancestor injector, above me in the injector hierarchy.'

By default, the injector throws an error when it can't find a requested provider. The `@Optional()` decorator means not finding the service is OK. The injector returns `null`, the `parentModule` parameter is `null`, and the constructor concludes uneventfully.

It's a different story if you improperly import `GreetingModule` into a lazy loaded module such as `CustomersModule`.

`Angular` creates a lazy loaded module with its own injector, a child of the root injector. `@SkipSelf()` causes `Angular` to look for a `GreetingModule` in the parent injector, which this time is the root injector. Of course it finds the instance imported by the root `AppModule`. Now `parentModule` exists and the constructor throws the error.

Here are the two files in their entirety for reference:

```ts
// app.module.ts
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';

/* App Root */
import { AppComponent } from './app.component';

/* Feature Modules */
import { ContactModule } from './contact/contact.module';
import { GreetingModule } from './greeting/greeting.module';

/* Routing Module */
import { AppRoutingModule } from './app-routing.module';

@NgModule({
  imports: [
    BrowserModule,
    ContactModule,
    GreetingModule.forRoot({userName: 'Miss Marple'}),
    AppRoutingModule
  ],
  declarations: [
    AppComponent
  ],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

```ts
// greeting.module.ts
import { ModuleWithProviders, NgModule, Optional, SkipSelf } from '@angular/core';

import { CommonModule } from '@angular/common';

import { GreetingComponent } from './greeting.component';
import { UserServiceConfig } from './user.service';


@NgModule({
  imports:      [ CommonModule ],
  declarations: [ GreetingComponent ],
  exports:      [ GreetingComponent ]
})
export class GreetingModule {
  constructor (@Optional() @SkipSelf() parentModule?: GreetingModule) {
    if (parentModule) {
      throw new Error(
        'GreetingModule is already loaded. Import it in the AppModule only');
    }
  }

  static forRoot(config: UserServiceConfig): ModuleWithProviders<GreetingModule> {
    return {
      ngModule: GreetingModule,
      providers: [
        {provide: UserServiceConfig, useValue: config }
      ]
    };
  }
}
```

---

[Angular Docs](https://angular.io/guide/singleton-services#prevent-reimport-of-the-greetingmodule)