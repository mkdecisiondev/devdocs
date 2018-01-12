# npm

npm is the default package manager for Node.js. [Yarn](https://yarnpkg.com/) is an alternative that works with `package.json` as well, but has some differences. Stick with npm until further notice.

# MK npm Registry
We have a private npm Registry used to host our own Node.js modules. To access
this registry, you'll need to configure npm to use and log in to it. It uses your
Github username and password to authenticate you.

Use the command below to log into the registry. You'll use your Github username
and password when prompted. If you use **Github Two-Factor Authentication** you'll
need to specify your username like: `jacob.123456` where the numbers are a current
2FA code.

```
npm login --scope=@mkdecision --registry=https://registry.mkdecision.com
```
