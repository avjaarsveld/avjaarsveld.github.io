---
layout: post
title: Useful Sublime Shortcuts and Commands
tags:
- sublime
- cheatsheet
- commands
---

I use this post to remind me of keyboard shortcut keys, etc, for the
`Sublime Text 2` editor. These are just reminders for functionality that I am already
somewhat familiar with, so there isn't much explanation, which is readily available
online.

> Work in progress. Comment if you think there is somehing I should list here.

## Selection

### Select Next

```
Ctrl D
```

### Select Block/Column

By default this is set to `ctrl+shift+up` and `ctrl+shift+down`, but that did not work on my MacBook as those keys are already used by OS X. I therefore changed it, as shown below, to `alt+shift+up` and `alt+shift+down`.

To edit `select_lines` in Sublime:

1. Go to **Preferences > Key Bindings - User**

2. Add or edit the following lines, so that they look like this:

```
  { "keys": ["alt+shift+up"], "command": "select_lines", "args": {"forward": false} },
  { "keys": ["alt+shift+down"], "command": "select_lines", "args": {"forward": true} }
```

> Check `Key Bindings - Default` to see what `select_lines` is set to by default.

## Quic Open a File

Mac: `CMD + P` | Ubuntu: `Ctrl + P`

Searches for a file in the current project based on the file name, press enter to open the selected file.

## The Basics

### Undo, Redo

```
Ctrl Z
Ctrl Shift Z
```
