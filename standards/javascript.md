# JavaScript coding standards

Follow the rules in the [ESLint configuration](https://github.com/mkdecisiondev/lintconfig/blob/master/.eslintrc.js).

The [Dojo style guide](https://github.com/dojo/meta/blob/master/STYLE.md) provides a lot of good guidance. There may be
some differences in our ESLint configuration, in that case those take precedence.

1. Use single quotes for string values, unless the string contains a single quote, in which case it is preferable to use
   double quotes and avoid escaping the single quotes in the content.
1. Only quote property names when necessary (e.g. if they contain a dash or begin with '0')
