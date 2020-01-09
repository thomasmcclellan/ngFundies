##### 1/07/2020
# Component Styles - View Encapsulation
As discussed earlier, component `CSS` style are encapsulate into the component's view and don't affect the rest of the application.

To control how this encapsulation happened on a _per component_ basis, you can't set the _view encapsulation mode_ in the component metadata.  Choose from the following modes:
  * `ShadowDom` view encapsulation uses the browser's native shadow `DOM` implementation (see [Shadow `DOM`](https://developer.mozilla.org/en-US/docs/Web/Web_Components/Using_shadow_DOM) on the [MDN](https://developer.mozilla.org/en-US/) site) to attach a shadow `DOM` to the component's host element, and then puts the components view inside that shadow `DOM`.  The component's styles are included within the shadow `DOM`.
  * `Native` view encapsulation uses a now deprecated version of the browser's native shadow `DOM` implementation - [learn about the changes](https://hayatoito.github.io/2016/shadowdomv1/)
  * `Emulated` view encapsulation (the default) emulates the behavior of shadow `DOM` by preprocessing (and renaming) the `CSS` code to effectively scope the `CSS` to the component's view
  * `None` means that `Angular` does no view encapsulation.  `Angular` adds the `CSS` to teh global styes.  the scoping rules, isolations, and protections discussed earlier don't apply.  This is essentially the same as pasting the component's styles into the `HTML`.

To set the component's encapsulation mode, use the `encapsulation` property in the component metadata:

```ts
// Warning: few browsers support shadow DOM encapsulation at this time
encapsulation: ViewEncapsulation.Native
```

`ShadowDom` view encapsulation only works on browsers that have native support for shadow `DOM`.  The support is still limited, which is why `Emulated` view encapsulation is the default mode and recommended in most cases.

---

[Angular Docs](https://angular.io/guide/component-styles#loading-component-styles)