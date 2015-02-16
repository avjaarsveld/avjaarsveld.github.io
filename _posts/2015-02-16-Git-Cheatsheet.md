---
layout: post
tags:
- git
- cheatsheet
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

> I always check online reference docs before attempting an undo as what you can do depends on where
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

## Save and Stash

```
git stash
git stash pop
```

### Save work with a name

```
git stash save -u "my_work"
```