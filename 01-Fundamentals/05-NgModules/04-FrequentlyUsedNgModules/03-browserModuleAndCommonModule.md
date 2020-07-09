##### 6/11/2020
# Frequently-Used Modules - `BrowserModule` and `CommonModule`
`BrowserModule` imports `CommonModule`, which contributes many common directives such as `ngIf` and `ngFor`. Additionally, `BrowserModule` re-exports `CommonModule` making all of its directives available to any module that imports `BrowserModule`.

For apps that run in the browser, import `BrowserModule` in the root `AppModule` because it provides services that are essential to launch and run a browser app. `BrowserModule`'s providers are for the whole app so it should only be in the root module, not in feature modules. Feature modules only need the common directives in `CommonModule`; they don’t need to re-install app-wide providers.

If you do import `BrowserModule` into a lazy loaded feature module, `Angular` returns an error telling you to use `CommonModule` instead.

![`BrowserModule` Error](../../../Assets/browserModuleError.gif)

---

[Angular Docs](https://angular.io/guide/frequent-ngmodules#browsermodule-and-commonmodule)