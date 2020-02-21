##### 1/17/2020
# `Angular` Elements - Example: A Popup Service
Previously, when you wanted to add a component to an app at runtime, you had to define a _dynamic component_.  The app module would have to list your dynamic component under `entryComponents`, so that the app wouldn't expect it to be present at startup, and then you would have to load it, attach it to an element in the `DOM`, and wire up all of the dependencies, change detection, and event handling, as described in [Dynamic Component Loader](https://angular.io/guide/dynamic-component-loader).

User an `Angular` custom element makes the process much simpler and more transparent, by providing all of the infrastructure and framework automatically--all you have to do is define the kind of event handling you want (You do still have to execute the component from compilation, if you ware not going to use it in your app).

The `Popup Service` example app defines a component that you can either load dynamically  or convert to a custom element.
  * `popup.component.ts` defines a simple pop-up element that displays an input message, with some animation and styling
  * `popup.service.ts` creates an injectable service that provides two different ways to invoke the `PopupComponent`; as a dynamic component, or as a custom element.  Notice how much more setup is required for the dynamic-loading method
  * `app.module.ts` adds the `PopupComponent` in the module's `entryComponent` list, to exclude it from compilation and avoid startup warnings or errors
  * `app.component.ts` defines the app's root component, which uses the `PopupService` to add the pop-up to the `DOM` at runtime.  When the app runs, the root component's constructor converts `PopupComponent` to a custom element.

For comparison, the demo shows both methods.  One button adds the popup using the dynamic-loading method, and the other uses the custom element.  You can see that the result is the same; only the preparation is different.

```ts
// popup.component.ts
import { Component, EventEmitter, Input, Output } from '@angular/core';
import { animate, state, style, transition, trigger } from '@angular/animations';

@Component({
  selector: 'my-popup',
  template: `
    <span>Popup: {{ message }}</span>
    <button (click)="closed.next()">&#x2716;</button>
  `,
  host: { '[@state]': 'state' },
  animations: [
    trigger('state', [
      state('opened', style({ transform: 'translateY(0)' })),
      state('void, closed', style({ transform: 'translateY(100%)', opacity: 0 })),
      transition('* => *', animate('100ms ease-in'))
    ])
  ],
  styles: [`
    :host {
      position: absolute;
      bottom: 0;
      left: 0;
      right: 0;
      background: #00cff;
      height: 49px;
      padding: 16px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      border-top: 1px solid black;
      font-size: 24px;
    }

    button {
      border-radius: 50%;
    }
  `]
})
export class PopupComponent {
  private state: 'opened' | 'closed' = 'closed'

  @Input() 
  set message(message: string) : void {
    this._message = message
    this.state = 'opened'
  }
  get message() : string { return this._message }
  _message: string

  @Output() closed = new EventEmitter()
}
```

```ts
// popup.service.ts
import { ApplicationRef, ComponentFactoryResolver, Injectable, Injector } from '@angular/core';
import { NgElement, WithProperties } from '@angular/elements';
import { PopupComponent } from './popup.component.ts';

@Injectable()
export class PopupService {
  constructor(
    private injector: Injector,
    private applicationRef: ApplicationRef,
    private componentFactoryResolver: ComponentFactoryResolver
  ) { }

  // Previous dynamic-loading method required you to set up infrastructure before adding the popup to the DOM
  showAsComponent(message: string) {
    // Create element
    const popup = document.createElement('popup-component')

    // Create the component and wire it up with the element
    const factory = this.componentFactoryResolver.resolveComponentFactory(PopupComponent)
    const popupComponentRef = factory.create(this.injector, [], popup)

    // Attach to the view so that the change detector knows to run
    this.applicationRef.attachView(popupComponentRef.hostView)

    // Listen to the close event
    popupComponentRef.instance.closed.subscribe(() => {
      document.body.removeChild(popup)
      this.applicationRef.detachView(popupComponentRef.hostView)
    })

    // Set the message
    popupComponentRef.instance.message = message

    // Add to the DOM
    document.body.appendChild(popup)
  }

  // This uses the new custom-element method to add the popup to the DOM
  showAsElement(message: string) : void {
    // Create element
    const popupEl: NgElement & WithProperties<PopupComponent> = document.createElement('popup-element') as any

    // Listen to the close event
    popupEl.addEventListener('closed', () =>  document.body.removeChild(popupEl))

    // Set the message
    popupEl.message = message

    // document.body.appendChild(popupEl)
  }
}
```

```ts
// app.module.ts
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { BrowserAnimationsModule } from '@angular/platform-browser/animations';

import { AppComponent } from './app.component';
import { PopupComponent } from './popup.component';
import { PopupService } from './popup.service';

// Include the 'PopupService' provider but exclude 'PopupComponent' from the compilation, because it will be added dynamically

@NgModule({
  imports: [BrowserModule, BrowserAnimationsModule],
  providers: [PopupService],
  declarations: [AppComponent, PopupComponent],
  bootstrap: [AppComponent],
  entryComponents: [PopupComponent]
})
export class AppModule { }
```

```ts
// app.component.ts
import { Component, Injector } from '@angular/core';
import { createCustomElement } from '@angular/elements';
import { PopupService } from './popup.service';
import { PopupComponent } from './popup.component';

@Component({
  selector: 'app-root',
  template: `
    <input #input value="Message">
    <button (click)="popup.showAsComponent(input.value)">Show as component</button>
    <button (click)="popup.showAsElement(input.value)">Show as element</button>
  `
})
export class AppComponent {
  constructor(injector: Injector, public popup: PopupService) {
    // Convert 'PopupComponent' to a custom element
    const PopupElement = createCustomElement(PopupComponent, { injector })

    // Register the custom element with the browser
    customElement.define('popup-element', PopupElement)
  }
}
```

---

[Angular Docs](https://angular.io/guide/elements#example-a-popup-service)