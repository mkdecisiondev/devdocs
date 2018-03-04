# Node.js

[Node.js](https://nodejs.org) was developed to run JavaScript outside a web browser. It has since become a valuable development tool allowing JavaScript code to run on your workstation and perform build-related tasks like code preprocessing and minification.

You should typically install the LTS release of Node.js, and periodically update it. Updating Node.js will automatically update [npm](npm.md), the Node.js package manager, as well. You can also manually update npm at any time:

```shell
npm install -g npm
```

If you are not writing your own Node.js applications then you don't need to learn Node's API.

## Installing Node.js with OS X

If you are a Mac user, you should ALWAYS be using brew to install Node.js if you have not already done so. If you managed to install Node.js without using brew, it is strongly suggested that you uninstall it and install it using brew. 

To install Node.js with brew, you need only enter the command `brew install node@8` (as of the time of writing, this is the LTS release, but if you want the most bleeding edge version, you can enter `brew install node`). That's it. You're done, and npm is installed with it. Whenever you run `brew update`, Node.js will update too. To switch between versions you can [refer to this article](https://medium.com/@katopz/how-to-install-specific-nodejs-version-c6e1cec8aa11).
