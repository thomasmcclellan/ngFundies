##### 6/12/2020
# Types of Feature Modules
There are five general categories of feature modules which tend to fall into the following groups:
  * Domain feature modules
  * Routed feature modules
  * Routing modules
  * Service feature modules
  * Widget feature modules

While the following guidelines describe the use of each type and their typical characteristics, in real world apps, you may see hybrids.

The following table summarizes the key characteristics of each feature module group.

| Feature Module | Declarations | Providers | Exports | Imported by |
|---|---|---|---|---|
| Domain | Yes | Rare | Top Component | Feature, `AppModule` |
| Routed | Yes | Rare | No | None |
| Routing | No | Yes (Guards) | `RouterModule` | Feature (for routing) |
| Service | No | Yes | No | `AppModule` |
| Widget | Yes | Rare | Yes | Feature |

---

[Angular Docs](https://angular.io/guide/module-types)