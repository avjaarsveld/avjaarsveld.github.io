---
layout: post
tags:
- git
- cheatsheet
- development
---

I use this as a quick reference for commands that I already know about (where I may have
forgotten the exact syntax etc), so there is therefore not a lot of explanation (which you can find
with a bit of googling if needed).

> If you see something that could be done better, let me know in the comments

## Normal Workflow

This is a typical workflow for me (though I don't always use all of these commands). See below for
some details about what each of these git commands do.

```
git checkout branch_name
```

```
git pull
```

```
git status
```

```
git checkout -b new_branch_name
```

```
git branch

```

~ do some work ~

```
git add .
```

```
git commit -am "Commit message"
```

```
git push -u origin new_branch_name
```

## Manual Merge Workflow

Checkout and update the branch that will be altered (merged into):

```
git checkout master
git pull
```

```
git merge other_branch
```

> If there are merge conflicts, use `git status` to see where they are, then edit those
> files to fix the conflicts.
> Once all conflicts have been resolved, run `git add` on the conflicted files followed
> by `git commit` to generate the merge commit.

## Checkout

### Checkout an old Commit

```
git checkout commit_reference
```

Use `git log` to get old commit references for the branch.

### Checkout a Particular File

```
git checkout origin/staging --filename
```

`origin/staging` can be a previous commit (use `git log`), etc.

### Checkout the Previous Branch

```
git checkout -
```

## Delete

### Delete a branch on local and github (remote)

```
git branch -d branch_name
git push origin :branch_name
```

## Rename

### Rename a branch on local and github (remote)

```
git branch -m old_branch_name new_branch_name
git push origin :new_branch_name
```

Now delete the old branch on github.

## Undo

> Check (online) reference docs before attempting an undo as what you can do depends on where
> in the process you are.

### Undo a merge

```
git merge --abort
```

### Undo a commit

```
git reset --soft 'HEAD^'
```

This undoes a commit without losing changes to files.

### Undo a Bundle Update

```
git checkout -- Gemfile.lock
```

Sometimes `Gemfile.lock` is updated by bundle, and whatever you do in git does not work as bundle keeps updating it (I do not want to push these changes to Gemfile.lock). In that case the following has worked for me (remove the file and fetch it again):

```
git rm -f Gemfile.lock
git fetch
git checkout FETCH_HEAD -- Gemfile.lock
```

## Upstream

### Set upstream branch

```
git branch --set-upstream local_branch_name
```

> This is not necessary if you have been using `push -u`

## Clone

```
git clone git@xyz.git new_folder_name
```

## History and Status

```
git log
```

```
git branch
```

```
git status
```

### What has been changed

> See [gitready.com/intermediate/2009/01/30/finding-what-has-been-changed.html](http://gitready.com/intermediate/2009/01/30/finding-what-has-been-changed.html)

```
git diff
```

## Save and Stash

```
git stash
git stash pop
```

### Save work with a name

```
git stash save -u "my_work"
```
