# NPM Cheat Sheet

List global packages on Level 0

```js
npm list -g -depth=1
```

### Use local packages

Path to the local packages

```js
> ls /usr/local/lib/node_modules
```

```js
// link package from package dir
npm link

// Install packages from your project dir
npm link <package_name>
```

Scoped packages

```js
// in package.json add scoped name
{
  "name": "@mycompany/fast-lib"
  // ...
}

// link package from package dir
npm link

// Install packages from your project dir
npm link <@scope>/<package_name>

// Include package in your project
import { <module> } from '@scope/package_name';
const { <module> } = require('@scope/package_name');
```

### Publishing packages to NPMjs

For the first time go into package dir and run

```js
// no scoped package will be public
npm publish

// to have public scope packages
npm publish --access=public
```

Update published package

```js
// Update version
npm version <new-version>
npm publish
```
