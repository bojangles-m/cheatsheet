# HomeBrew

### List installed packages

```shell
$ brew list
```

### How do I list available versions?

```shell
$ brew search <package-name>
```

### List all outdated formulae and cask.

```shell
$ brew outdated
```

### Misc

```shell
$ brew update   # updates brew itself
$ brew upgrade  # upgrades all packages installed via brew
$ brew cleanup  # by default, brew doesn't uninstall old versions. cleanup command will do the job
$ brew doctor   # Checks brew state and returns error, if there are any issues
```
