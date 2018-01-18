# Best practices: JavaScript

## Documentation comments

Documentation comments can make code easier to understand and use. Comments should not explain what code does - the
code itself should explain what it does! Use descriptive names for functions and variables, and write code in a simple,
straightforward manner that makes the flow of logic clear. Comments should be added to clarify external factors that
affect the code, like bugs that are being worked around.

If code needs additional documentation to clarify usage and provide examples, do so in an associated Markdown file.

## Use JSDoc

[JSDoc](http://usejsdoc.org/) can parse correctly
formatted comments and generate API documentation files as HTML. Visual Studio Code can also parse JSDoc comments
and provide code completion and API info.

A few important aspects of JSDoc to understand:

* [Classes](http://usejsdoc.org/howto-es2015-classes.html)
* [Modules](http://usejsdoc.org/howto-es2015-modules.html)
* [Typedefs](http://usejsdoc.org/tags-typedef.html)
