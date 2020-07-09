##### 6/18/2020
# Entry Components - The `entryComponents` `Array`
Though the `@NgModule` decorator has an `entryComponents` array, most of the time you won't have to explicitly set any entry components because `Angular` adds components listed in `@NgModule.bootstrap` and those in route definitions to entry components automatically. Though these two mechanisms account for most entry components, if your app happens to bootstrap or dynamically load a component by type imperatively, you must add it to `entryComponents` explicitly.

---

## `entryComponents` and the Compiler:
For production apps you want to load the smallest code possible. The code should contain only the `classes` that you actually need and exclude components that are never used. For this reason, the `Angular` compiler only generates code for components which are reachable from the `entryComponents`; This means that adding more references to `@NgModule.declarations` does not imply that they will necessarily be included in the final bundle.

In fact, many libraries declare and export components you'll never use. For example, a material design library will export all components because it doesn’t know which ones you will use. However, it is unlikely that you will use them all. For the ones you don't reference, the tree shaker drops these components from the final code package.

If a component isn't an entry component and isn't found in a template, the tree shaker will throw it away. So, it's best to add only the components that are truly entry components to help keep your app as trim as possible.

---

[Angular Docs](https://angular.io/guide/entry-components#the-entrycomponents-array)