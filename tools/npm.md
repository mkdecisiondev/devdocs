# npm

npm is the default package manager for Node.js. [Yarn](https://yarnpkg.com/) is an alternative that works with `package.json` as well, but has some differences. Stick with npm until further notice.

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
