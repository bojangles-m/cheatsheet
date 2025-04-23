# Git Cheat Sheet

## Setup git

```js
# setup global file
$ git config --global core.excludesfile ~/.gitignore
```

## Commands

Unstage files or remove from git cache

```js
$ git rm --cached .DS_Store
```

Delete branch

```js
$ git branch -D <branch name>
```

New branch and checkout new branch

```js
$ git checkout -b <new branch name>
```

Changes to last commit

```js
// Add staged changes to last commit
$ git commit --amend

// Change last commit message
$ git commit --amend -m "New commit message"
```

Revert commit without losing changes

```js
$ git reset HEAD~1
```

Rebase onto branch master

```js
$ git rebase master
```

Squash 3 commits

```js
$ git rebase -i HEAD~3
```

List of changed files between master and branch

```js
$ git diff --name-only master
```

Unstage file

```js
$ git reset <file_name>
```

Discard local changes

```js
$ git reset HEAD <file_name>;
$ git checkout <file_name>
```

Force push to origin

```js
$ git push origin <branch_name> --force
```

Deleted file but didn’t commit - needs to be staged

```js
$ git checkout HEAD <filename>
```

### Fresh branch from remote

All local changes will be wiped and overwritten by remote branch

```js
$ git reset --heard origin/<branch name>
```

### How to narrow down where bug occurs

The bug was create and now it is time to find the most recent commit without bug

```js
$ git bisect start
$ git bisect bad         # set bad is my recent commit
$ git bisect good <hash> # most recent commit without bug
# After 'good 'the next commit between this edges is picked to test
$git bisect bad          # the picked one had a bug
$git bisect good         # this one is good and the bug dont exist in this commit
# at this point you get the message and hash so you can go back and compare the codes and find the bug
```

### Info about branch and remove branch that don't exist remote

```js
$ git branch -vv
```

Flag branches not existing remote

```js
$ git remote update --prune
```

Print branch name we are searching for

```js
$ git branch -vv | awk '/: gone]/{print $1}'
```

Remove branches that get returned as a search result

```js
$ git branch -vv | awk '/: gone]/{print $1}' | xargs git branch -d
```

### Logging

```js
$ git reflog
```

```js
$ git log --graph --decorate --oneline
```

### Tagging

```js
// list tags
git tag -l

// remove tag
$ git tag -d <tag_name>
```

### Troubles with files

```js
git config core.ignorecase false
git rm -r --cache src/js
git add -A src/js
git commit -m 'capitalize files'
git push
```

### Troubles with git HOOKS

Try to configure the Hooks path

```js
git config core.hooksPath .git/hooks/
```

### List config

```sh
$ git config -l
```

## Move stashed Git changes from one Mac to another

1. On the source Mac (where the stash is): This saves the stashed diff into a patch file.

```sh
git stash show -p > stash.patch
```

2. Transfer stash.patch to the other Mac

3. On the target Mac (in the same repo): your stash changes are applied to your working directory!

```sh
git apply stash.patch
```

## Move multiple git branches from one to another without pushing them to the origin server

1. On the Source Computer navigate to the repo and create bundle file

```sh
git bundle create <prs.bundle> feature/one feature/two bugfix/three
```

This creates a prs.bundle file that includes those branches and all their commit history.

2. Transfer the Bundle to the target computer where you can:

a. Verify the bundle (optional):

```sh
git bundle verify /path/to/prs.bundle
```

b. Fetch from the bundle and create a local branch with the same name.

```sh
git fetch /path/to/prs.bundle branch-name:branch-name
```
