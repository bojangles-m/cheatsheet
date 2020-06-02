# Yarn Cheat Sheet

## Symlink a package folder during development.

Go into package folder and run command

```sh
$ yarn link
```

After go into project folder where you need this package and run:

```sh
$ yarn link "<name of package>"
```

When you are done remove it! Go to package folder and:

```sh
$ yarn unlink
```
