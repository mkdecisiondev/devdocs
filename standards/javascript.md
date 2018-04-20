# JavaScript coding standards

Follow the rules in the [ESLint configuration](https://github.com/mkdecisiondev/lintconfig/blob/master/.eslintrc.js).

The [Dojo style guide](https://github.com/dojo/meta/blob/master/STYLE.md) provides a lot of good guidance. There may be
some differences in our ESLint configuration, in that case those take precedence.

1. Use single quotes for string values, unless the string contains a single quote, in which case it is preferable to use
	double quotes and avoid escaping the single quotes in the content.
1. Only quote property names when necessary (e.g. if they contain a dash or begin with '0')

## Modules

1. Module names should be camel cased
1. Modules that primarily export a class should have the same name as the class (which should be CamelCase)
1. Modules that do not export a class should have a descriptive name starting with lower case (camelCase)
1. Modules should use named exports instead of default exports ([further reading](https://blog.neufund.org/why-we-have-banned-default-exports-and-you-should-do-the-same-d51fdc2cf2ad)), e.g.:

```javascript
class MyClass {}
export { MyClass };
```
