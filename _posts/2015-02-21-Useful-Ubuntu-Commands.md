---
layout: post
title: Useful Ubuntu Commands
tagline: This is a work in progress...
tags:
- Ubuntu
- Terminal
---

> This post is a work in progress. Comment if you think I should add anything.

## Find

### Search within files

```
ack-grep -i "search string with.*regex"
```

### Find a file by filename

> See [help.ubuntu.com/community/FindingFiles](https://help.ubuntu.com/community/FindingFiles)

```
find ~/my-dir/ -iname '*.moo'
```

```
sudo find /rootdir/ -iname 'moo.*'
```

## System Configuration

### Screen Brightness

```
sudo intel_backlight 40
```

The above command sets the screen brightness to 40%.

