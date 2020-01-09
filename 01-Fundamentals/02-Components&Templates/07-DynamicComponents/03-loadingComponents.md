##### 1/08/2020
# Dynamic Components - Loading Components
Most of the ad banner implementation is in `ad-banner.component.ts`.  To keep things simple in this example, the `HTML` is in the `@Component` decorator's `template` property as a template `string`.

The `<ng-template>` element is where you apply the directive you just made.  To apply the `AdDirective`, recall the selector from `ad.directive.ts`, `ad-host`.  Apply that to `<ng-template>` without the square brackets.  Now `Angular` knows where to dynamically load components.

```ts
template: `
  <div class="ad-banner-example">
    <h3>Advertisement</h3>
    <ng-template ad-host></ng-template>
  </div>
`
```

The `<ng-template>` element is a good choice for dynamic components because it doesn't render any additional output.

---

[Angular Docs](https://angular.io/guide/dynamic-component-loader#loading-components)