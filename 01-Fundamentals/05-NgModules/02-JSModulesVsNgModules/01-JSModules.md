##### 6/01/2020
# `JavaScript` Modules vs. NgModules - `JavaScript` Modules
In `JS`, modules are individual files with `JS` code in them.  To make what's in them available, you write an export statement, usually after the relevant code like this:

```ts
export class AppComponent { ... }
```

Then, when you need that file's code in another file, you import it like this:

```ts
import { AppComponent } from './app.component';
```

`JS` modules help you namespace, preventing accidental global variables.

---

[Angular Docs](https://angular.io/guide/ngmodules#the-basic-ngmodule)