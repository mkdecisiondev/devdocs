# npm

:poop: npm is the default package manager for Node.js. It is not well designed so [pnpm](https://pnpm.js.org/) should typically be used instead:
```
npm install --global pnpm
```

Once pnpm is installed you should use it in place of `npm` - any time you would use `npm`, type `pnpm` instead. The exception is for global modules - when you are installing something globally ([eslint](https://www.npmjs.com/package/eslint), [htmlhint](https://www.npmjs.com/package/htmlhint), [http-serve](https://www.npmjs.com/package/http-serve)) you should use `npm i -g <module>` to install or update it (this includes pnpm - use npm to update pnpm).

# MK npm registry

We have a private npm registry used to host packages from our private repositories. To access
this registry you'll need to configure npm to use and log in to it. It uses your
GitHub username and password to authenticate you.

Use the command below to log in to the registry. You'll use your GitHub username
and password when prompted. If you use [two-factor authentication](https://help.github.com/articles/about-two-factor-authentication/) you'll
need to specify your username like: `username.123456` where the numbers are a current
2FA code.

```
npm login --scope=@mkdecision --registry=https://registry.mkdecision.com
```
