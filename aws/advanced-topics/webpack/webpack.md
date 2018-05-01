# Setting Up Webpack in a Repository

When using AWS, it is useful to write functions and designate resources in a local repository, then to use a command line script to deploy functions and set up the resources with the relevant AWS services all at once. This can be done with AWS's CloudFormation service via the AWS command line interface. However, before you can use CloudFormation in this way, it is important to have the repository set up to use Babel and Webpack.

## Babel

JavaScript has had improvements and new features added over the years, such as with ES6, the version of JavaScript released in 2015. However, depending on where the code is run (such as in a browser), its environment may not understand these newer features, and the code will not run properly. This problem can be solved via the use of transpilers, such as Babel.js. This allows the newer code to be translated into language that its environment can handle. Let's look at an example, using Babel's [web console](https://babeljs.io/repl/):

We will write a very simple function, but use ES6 syntax:

```javascript
const greet = (name) => {
	return 'hello ' + name;
}
```

If we put this into Babel, here's what we get:

```javascript
'use strict';

var greet = function greet(name) {
	return 'hello ' + name;
};
```

All of the newer features we initially used, such as const and arrow functions, have been replaced with the pre-ES6 conventions. Babel has translated our newer-style code into JavaScript that can be run even in environments and browsers that don't support ES6. Not only is this useful for client-side JavaScript, it also can be used for AWS Lambda, as at any given time AWS may not support the most up-to-date version of JavaScript.

## Webpack

Webpack is a module builder that can be used to bundle a project. It will create a build directory, that, in the case of Lambda functions, will bundle every handler function and all its dependencies into a single file. This file can then be deployed to Lambda. When used alongside Babel, Webpack will also transpile the function and the module it builds will be compatiple with environments that are not compatible with ES6.
