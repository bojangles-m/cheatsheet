# NPMjs Cheat Sheet

## <i>IMPORTANT - ASDF</i>

If you use asdf package manager and some global packages are installed or packages are linked Reshim needs to be executed!!!!

```js
$ asdf reshim
```

<hr />

To check whether a package is installed

```js
npm ls --global foo
```

In order to uninstall the globally linked foo package, the following command can be used:

```js
sudo npm rm --global foo
```

List global packages on Level 0

```js
$ npm list -g -depth=1
```

### Use local packages

Path to the local packages

```js
$ ls /usr/local/lib/node_modules
```

```js
// link package from package dir
$ npm link

// Install packages from your project dir
$ npm link <package_name>
```

Scoped packages

```js
// in package.json add scoped name
{
  "name": "@mycompany/fast-lib"
  // ...
}

// link package from package dir
$ npm link

// Install packages from your project dir
$ npm link <@scope>/<package_name>

// Include package in your project
import { <module> } from '@scope/package_name';
const { <module> } = require('@scope/package_name');
```

### Publishing packages to NPMjs

For the first time go into package dir and run

```js
// no scoped package will be public
$ npm publish

// to have public scope packages
$ npm publish --access=public
```

Update published package

```js
// Update version
$ npm version [<newversion> | major | minor | patch | premajor | preminor | prepatch | prerelease [--preid=<prerelease-id>] | from-git]
$ npm publish
```

Inspect package version

```js
# to view a package''s published version
$ npm view <pkg> version

# to inspect current package/dependency versions
$ npm ls
```
