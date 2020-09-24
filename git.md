# Git Cheat Sheet

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

Rebase into branch master

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

Tagging

```js
// list tags
git tag -l

// remove tag
$ git tag -d <tag_name>
```
