##### 1/08/2020
# Dynamic Components - Resolving Components
Take a closer look at the methods in `ad-banner.component.ts`.

`AdBannerComponent` takes an `array` of `AdItem` `objects` as input, which ultimately comes from `AdService`.  `AdItem` `objects` specify the type of component to load and any data bind to the component.  `AdService` returns the actual ads making up the ad campaign.

Passing an `array` of components to `AdBannerComponent` allows for a dynamic list of ads without static elements in the template.

With its `getAds()` method, `AdBannerComponent` cycles through the `array` of `AdItems` and loads a new component every 3 seconds by calling `loadComponent()`.

```ts
export class AdBannerComponent implements OnInit, OnDestroy {
  @Input() ads: AdItem[]
  @ViewChild(AdDirective, { static: true }) adHost: AdDirective
  
  currentAdIndex: number = -1
  interval: any

  constructor(private componentFactoryResolver: ComponentFactoryResolver) { }

  ngOnInit() {
    this.loadComponent()
    this.getAds()
  }

  loadComponent() : void {
    this.currentAdIndex = (this.currentAdIndex + 1) % this.ads.length
    const adItem = this.ads[this.currentAdIndex],
          componentFactory = this.componentFactoryResolver.resolveComponentFactory(adItem.component),
          viewContainerRef = this.adHost.viewContainerRef
    viewContainerRef.clear()

    const componentRef = viewContainerRef.createComponent(componentFactory)
    
    (<AdComponent>componentRef.instance).data = adItem.data
  }

  getAds() : void {
    this.interval = setInterval(() => this.loadComponent(), 3000)
  }

  ngOnDestroy() {
    clearInterval(this.interval)
  }
}
```

The `loadComponent()` method is doing a lot of the heavy lifting here.  Take it step by step.  First, it picks an ad.

  > **How `loadComponent()` chooses an ad**
  >
  > The `loadComponent()` method chooses an ad using some math
  > 
  > first, it sets the `currentAdIndex` by taking whatever it currently is plus one, dividing that by the length of the `AdItem` `array`, and using the _remainder_ as the new `currentAdIndex` value.  Then, it uses that value to select an `adItem` from the `array`.

After `loadComponent()` selects an ad, it uses `ComponentFactoryResolver` to resolve a `ComponentFactory` for each specific component.  The `ComponentFactory` then creates an instance of each component.

Next, you're targeting the `viewContainerRef` that exists on the specific instance of the component.  How do you know it's this specific instance?  Because it's referring to `adHost` and `adHost` is the directive you set up earlier to tell `Angular` where to insert dynamic components.

As you may recall, `AdDirective` injects `ViewContainerRef` into its constructor.  This is how the directive accesses the element that you want to use to host the dynamic component.

To add the component to the template, you call `createComponent()` on `ViewContainerRef`.

The `createComponent()` method returns a reference to the loaded component.  Use that reference to interact with the component by assigning to its properties or calling its methods.

## Selector References: 
Generally, the `Angular` compiler generates a `ComponentFactory` for any component referenced in a template.  however, there are no selector references in the templates for dynamically loaded components since they load at runtime.

To ensure that the compiler still generates a factory, add dynamically loaded components to the `NgModel`'s `entryComponents` `array`.

```ts
entryComponents: [ HeroJobAdComponent, HeroProfileComponent ],
```

---

[Angular Docs](https://angular.io/guide/dynamic-component-loader#resolving-components)