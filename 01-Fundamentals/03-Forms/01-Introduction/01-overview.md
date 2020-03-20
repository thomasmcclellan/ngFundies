##### 2/28/2020
# Forms Introduction - Overview
Handling user input with forms is the cornerstone of many common applications.  Applications use forms to enable user to log in, to update a profile, to enter sensitive information, and to perform many other data-entry tasks.

`Angular` provides two different approaches to handling user input through forms:  _reactive_ and _template-driven_.  Both capture user input events from the view, validate the user input, create a form model and data model to update, and provide a way to track changes.

Reactive and template-driven forms process and manage form data differently.  Each other advantages.

In general:
  * **Reactive forms** are more robust:  they are  more scalable, reusable, and testable.  If forms are a key part of your application, or you're already using reactive patterns for building your application, use reactive forms.
  * **Template-driven forms** are useful for adding a simple form to an app, such as an email list signup form.  They're easy to add to an app, but they don't scale as well as reactive forms.  If you have very basic form requirements and logic that can be managed solely in the template, use template-driven forms.

This guide provides information to help you decide which type of form works best for your situation.  It introduces the common building blocks used by both approaches.  It also summarizes the key differences between the two approaches, and demonstrates those differences in the context of setup, data flow, and testing.
  
---

[Angular Docs](https://angular.io/guide/forms-overview)