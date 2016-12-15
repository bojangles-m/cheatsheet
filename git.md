# Git Cheat Sheet

Delete branch

```
$ git branch -D <branch name>
```

New branch and checkout new branch

```
$ git checkout -b <new branch name>
```

Change last commit

```
$ git commit --amend
$ git commit --amend -m "New commit message"
```

Revert commit without losing changes

```
$ git reset HEAD~1
```

Rebase into branch master

```
$ git rebase master
```

Squash 3 commits

```
$ git rebase -i HEAD~3
```

List of changed files between master and branch

```
$ git diff --name-only master
```

Unstage file

```
$ git reset <file_name>
```

Discard local changes

```
$ git reset HEAD <file_name>;
$ git checkout <file_name>
```

Force push to origin

```
$ git push origin <branch_name> --force
```

Deleted file but didn’t commit - needs to be staged

```
$ git checkout HEAD <filename>
```
