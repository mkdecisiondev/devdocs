# HTML coding standards

Follow the rules in the [HTMLHint configuration](https://github.com/mkdecisiondev/lintconfig/blob/master/.htmlhintrc).

## Formatting

1. Always use lowercase for tag and attribute names
1. Always use double quotes for attributes
1. `id`: value should be camel-case
    1. should be used sparingly, primarily for obtaining a reference to a node in JS
1. `class`: value should be dasherized

## File names

1. HTML files that will be served over HTTP should be named in lowercase dasherized
1. HTML files that are templates to be consumed by other modules, and that will never be served over HTTP should be named camel-case (same as JavaScript modules).
