# npm

:poop: npm is the default package manager for Node.js. It is not as optimized as
alternative package managers, we use [Yarn](https://yarnpkg.com/en/). There are
many ways to install yarn on different systems, but the easiest is through npm:

```bash
npm install -g yarn
```

You should use Yarn in any place you would use npm. You should node these differences:
`npm install` is `yarn add`, and to install global packages you should use
`yarn global add [package]`

## MK npm registry

We have a private npm registry used to host packages from our private repositories. To access
this registry you'll need to configure npm to use and log in to it. It uses Github
to authenticate you

Go to https://registry.mkdecision.com and hit Login at the top right. Once you've
authorized the Github app, you'll be redirected back to the main page where you'll
see two commands in the header like below:

![import-gradle.png](img/npm-registry-header.png)

Enter those commands in a console followed by this last command:

```bash
npm config set registry https://registry.mkdecision.com
```

The first two commands will configure authentication with the registry so that
you can access it. The last will set it as your default repository.