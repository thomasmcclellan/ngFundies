##### 9/13/2019
# Introduction to Components - Component Metadata
The `@Component` decorator identifies the class immediately below it as a component class, and specifies its metadata.  In the example code below, you can see that `HeroListComponent` is just a class, with no special `Angular` notation or syntax at all.  It's not a component until you mark it as one with the `@Component` decorator.

The metadata for a component tells `Angular` where to get the major building blocks that it needs to create and present the component and its view.  In particular, it associates a _template_ with the component, either directly with inline code, or by reference.  Together, the component and its template describe a _view_.

In addition to containing or pointing to the template, the `@Component` metadata configures, for example, how the component can be referenced in `HTML` and what services it requires.  

`src/app/hero-list.component.ts` (metadata):
```typescript
@Component({
  selector: 'app-hero-list',
  templateUrl: './hero-list.component.html',
  providers: [ HeroService ]
})
export class HeroListComponent implements OnInit {
  ...
}
```

This example shows some of the most useful `@Component` configuration options:

| Metadata | Description |
|---|---|
| `selector` | A `CSS` selector that tells `Angular` to create and insert and instance of this component wherever it finds the corresponding tag in template `HTML`. |
| `templateUrl` | The module-relative address of this component's `HTML` template.  Alternatively, you can provide the `HTML` template inline, as the value of the `template` property.  This template defines the component's _host view_. |
| `providers` | An `array` of [providers](https://angular.io/guide/glossary#provider) for services that the component requires. |

---

[Angular Docs](https://angular.io/guide/architecture-components)