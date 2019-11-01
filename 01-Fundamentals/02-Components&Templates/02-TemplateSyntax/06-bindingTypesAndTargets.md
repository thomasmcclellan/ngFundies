##### 10/08/2019
# Template Syntax - Binding Types and Targets
The target of a **data-binding** is something in the `DOM`.  Depending on the binding type, the target can be a property (element, component, or directive), an event (element, component, or directive), or sometimes an attribute name.  The following table summarizes the targets for the different binding types:

| Type | Target | Examples |
|---|---|---|
| Property | Element property<br>Component property<br>Directive property | `src`, `hero`, and `ngClass` in the following:<br><pre><img [src]="heroImageUrl"><br><app-hero-detail [hero]="currentHero"></app-hero-detail><br><div [ngClass]="{ 'special': isSpecial }"></div></pre> |
| Event | Element event<br>Component event<br>Directive event | `click`, `deleteRequest`, and `myClick` in the following:<b><pre><button (click)="onSave()">Save</button><br><app-hero-detail (deleteRequest)="deleteHero()"></app-hero-detail><br><div (myClick)="clicked=$event" clickable>Click Me</div></pre> |
| Two-way | Event and property | <pre><input [(ngModel)]="name"></pre> |
| Attribute | Attribute (the exception) | <pre><button [attr.aria-label]="help">Help</button></pre> |
| Class | `class` property | <pre><div [class.special]="isSpecial">Special</div></pre> |
| Style | `style` property | <pre><button [style.color]="isSpecial ? 'red' : 'green'"></pre> |

---

[Angular Docs](https://angular.io/guide/template-syntax#binding-types-and-targets)