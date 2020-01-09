##### 1/08/2020
# Dynamic Components - Dynamic Component Loader
Component templates are not always fixed.  An application may need to load new components at runtime.

This cookbook shows you how to use `ComponentFactoryResolver` to add components dynamically.

## Dynamic Component Loading:
The following example show how to build a dynamic ad banner.

The hero agency is planning an ad campaign with several different ads cycling through the banner.  New ad components are added frequently by several different teams.  This makes it impractical to use a template with a static component structure.

Instead, you need a way to load a new component without a fixed reference to the component in the ad banner's template.

`Angular` comes with its own API for loading components dynamically.

---

[Angular Docs](https://angular.io/guide/component-styles#loading-component-styles)