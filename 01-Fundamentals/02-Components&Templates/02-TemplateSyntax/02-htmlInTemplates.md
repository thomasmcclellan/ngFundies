##### 10/03/2019
# Template Syntax - HTML in Templates
`HTML` is the language of the `Angular` template.  Almost all `HTML` syntax is valid template syntax.  The `<script>` element is a notable exception; it is forbidden, eliminating the rest of script injection attacks.  In practice, `<script>` is ignored and a warning appears in the browser console.

Some legal `HTML` doesn't make much sense in a template.  The `<html>`, `<body>`, and `<base>` elements have no useful role.  Pretty much everything else is fair game.

You can extend the `HTML` vocabulary of your template with components and directives that appear as new elements and attributes.  In the following sections, you'll learn how to get and set `DOM` values dynamically through data binding.

---

[Angular Docs](https://angular.io/guide/template-syntax)