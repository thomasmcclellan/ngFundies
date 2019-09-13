##### 9/09/2019
# Introduction to Modules - NgModule and Components
**NgModules** provide a _compilation context_ for their components.  A _root_ NgModule always has a root component that is created during **bootstrap**, but any NgModule can include any number of additional components, which can be loaded through the router or created through the template.  The components that belong to an NgModule share a compilation context.

```
NgModule A
  Root Component A
    A1
    A2
    A3

NgModule B
  Root Component B
    B1
    B2
    B3
```

A component and its template together define a **view**.  A component can contain a _view hierarchy-, which allow you to define arbitrarily complex areas of the screen that can be created, modified, and destroyed as a unit.  A view hierarchy can mix views defined in components that belong to different NgModules.  This is often the case, especially for UI libraries.

```
Host View Component A
  Embedded View A1
    Embedded View B1
    Embedded View B2
    Embedded View A3
  Embedded View A2
  Embedded View B3
```

When you create a component, it's associated directly with a single view, called the _host view_.  The host view can be the root of a view hierarchy, which can contain _embedded views_, which are in turn the host views of other components.  Those components can be in the same NgModule, or can be imported from other NgModules.  Views in the tree can be nested to any depth.

  > **NOTE**: The hierarchal structure of views is a key factor in the way `Angular` detects and responds to changes in the DOM and app data.

---

[Angular Docs](https://angular.io/guide/architecture-modules)