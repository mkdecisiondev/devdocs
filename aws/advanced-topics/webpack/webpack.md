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

## Setting Up Repository and Adding Dependencies

We'll start by initializing a repository using pnpm, the package manager of choice for MK Decision. This guide will assume that pnpm is already installed globally.

Create a project directory, and in it, using the command line run `$ pnpm init `. Follow the prompts (you can use the default values for all of the setup questions if desired). You will now have a package.json file.

In the project directory, add a folder called `services`. This will be where we write our handler functions. In that folder also create a subfolder called `lib`, where we will write helper functions that are used by the handlers. These will be bundled together with the handlers that import them when Webpack runs.

Let's install some dependencies. Our example repository will use [TypeScript](https://www.typescriptlang.org/), as this adds useful features to JavaScript and is especially helpful for keeping track of complicated data structures. TypeScript is not required for using any of the other tools covered in this guide, but if you intend to use TypeScript on a project, it is a good idea to set it up early. To install TypeScript, use the command `$ pnpm install typescript --save` (you can also use `i` as an abbreviation for `install`). If you are not planning to use Typescript, use `.js` as a file extension any time this guide uses `.ts`.

The other dependency that is required for production is Source Map Support. This is important for Webpack, and setting it up will be a necessary configuration step. Install it with `$ pnpm i source-map-support --save`.

All other dependencies we install, including all of the ones we need for Webpack and Babel, are dev dependencies. None of these tools will actually be used when the code is in production, but many of them are important to get it to production status.

We must install a number of types so that Typescript recognizes some of the tools we will use and does not throw errors when we are writing our code or running webpack to create our build. One command will install most of the ones that should be necessary: `$ pnpm i @types/body-parser @types/cors @types/dotenv @types/es6-promisify @types/node --save-dev`. If you are planning to write tests using Jest, you should also install `@types/jest` in the same way.

Next we'll install Webpack and its command line interface so we can write scripts using it: `$ pnpm i webpack webpack-cli --save-dev`.

ts-loader allows TypeScript to interact properly with Webpack: `$ pnpm i ts-loader --save-dev`.

Finally let's install all the dev dependencies we'll need for Babel: `$ pnpm i babel-core babel-loader babel-plugin-transform-async-to-generator babel-plugin-transform-es2015-modules-commonjs babel-preset-env --save-dev`.

## Setting Up Babel and Webpack

In the main project directory, create a file called `.babelrc`. This is where we configure the settings for Babel. Here is what we'll have in that file:

```json
{
	"presets": [
		[
			"env",
			{
				"targets": {
					"node": 8
				}
			}
		]
	],
	"plugins": [
		"transform-async-to-generator"
	]
}
```

There are a couple of important things to note: the `"node": 8` line indicates that we'll be transpiling our JavaScript into Node version 8. As of May 2018, this is the latest version of Node that Lambda supports.

The `transform-async-to-generator` plugin that we installed earlier is being used here. Async functions are an extremely convenient, but very recently added, tool to write asynchronous code. This plugin ensures that any instances of async functions will be transpiled into an older syntax.

We also need to add a configuration file for the source-map-support dependency. in `/services/lib/`, add a file called sourceMapSupports.ts. This file only needs one line:
```javascript
require('source-map-support').install();
```
