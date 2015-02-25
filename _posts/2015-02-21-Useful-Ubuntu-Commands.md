---
title: Useful Ubuntu Commands
tagline: This is a work in progress...
tags:
- Ubuntu
---

> This post is nowhere near complete.

## Find

### Search within files

```
ack-grep -i "search string with.*regex"
```

### Fina a file by filename

> See [help.ubuntu.com/community/FindingFiles](https://help.ubuntu.com/community/FindingFiles)

```
find ~/my-dir/ -iname '*.moo'
```

```
sudo find /rootdir/ -iname 'moo.*'
```

