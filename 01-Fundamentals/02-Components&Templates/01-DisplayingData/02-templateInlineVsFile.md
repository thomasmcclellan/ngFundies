##### 9/26/2019
# Introduction to Displaying Data - Template Inline or Template File?
You can store you component's **template** in one of two places.  YOu can define it _inline_ using the `template` property, or can you define the template in a separate `HTML` file and link to it in the component metadata using the `@Component` decorator's `templateUrl` property.

The choice between inline and separate `HTML` is a matter of taste, circumstances, and organizational policy. 

  > **NOTE**: If you use template _inline_, you will use the `template` property; not the `templateUrl` one.  Furthermore, if you use inline, you can either have you `HTML` in one line, using any form of `string` representation (single or double quotes, or back ticks), or break into multi-line `HTML` with back ticks.

In either style, the template data bindings have the same access to the component's properties.

  > By default, the `Angular CLI` command `ng generate component` generates components with a template file.  You can override that with something like this:
  > ``` 
  > ng g c hero -it 
  > ```

---

[Angular Docs](https://angular.io/guide/displaying-data)