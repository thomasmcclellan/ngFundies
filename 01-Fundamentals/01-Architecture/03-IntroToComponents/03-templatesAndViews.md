##### 9/16/2019
# Introduction to Components - Templates and Views
You define a component's **view** with its companion template.  A template is a form of `HTML` that tells `Angular` how to render the component.

Views are typically arranged hierarchically, allow you to modify or show and hide entire UI sections or pages as a unit.  The template immediately associated with a component defines that component's _host view_.  The component can also define a _view hierarchy_, which contains _embedded views_, hosted by other components.

A view hierarchy can include views from components in the same **NgModule**, but it also can (and often does) include views from components that are defined in different NgModules.

---

[Angular Docs](https://angular.io/guide/architecture-components)