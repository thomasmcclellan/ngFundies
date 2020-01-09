##### 1/09/2020
# Dynamic Components - The _AdComponent_ Interface
In the ad banner, all components implement a common `AdComponent` interface to standardize the API for passing data to the components.

Here are two sample components and the `AdComponent` interface for reference: 

```ts
// hero-job-ad.component.ts
import { Component, Input } from '@angular/core';
import { AdComponent } from './ad.component';

@Component({
  template: `
    <div class="job-ad">
      <h4>{{ data.headline }}</h4>
      {{ data.body }}
    </div>
  `
})
export class HeroJobComponent implements AdComponent {
  @Input() data: any
}
```

```ts
// hero-profile.component.ts
import { Component, Input } from '@angular/core';
import { AdComponent } from './ad.component';

@Component({
  template: `
    <div class="hero-profile">
      <h3>Featured Hero Profile</h3>
      <h4>{{ data.name }}</h4>
      <p>{{ data.bio }}</p>
      <strong>Hire this hero today!</strong>
    </div>
  `
})
export class HeroProfileComponent implements AdComponent {
  @Input() data: any
}
```

```ts
// ad.component.ts
export interface AdComponent {
  data: any
}
```

## Final Ad Banner:
The final ad banner looks like this:

![Final Ad Banner](../../../Assets/adBannerDemo.gif)


---

[Angular Docs](https://angular.io/guide/dynamic-component-loader#the-adcomponent-interface)