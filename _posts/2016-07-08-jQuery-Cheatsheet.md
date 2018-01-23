---
layout: post
tags:
- jQuery
- JavaScript
- Code Snippets
- Development
---

Some notes and reminders for jQuery

## Check if Array contains something

```
if (obj.indexOf('widgetID') != -1) {
  // widgetID not found in obj
}
```

## Optional Variables for Function with Default Values

```
function filename_truncated(name, appendage, max_length, char_length) {
  // appendage, max_length and char_length are optional with default values
  appendage = typeof appendage !== 'undefined' ? appendage : '...';
  max_length = typeof max_length !== 'undefined' ? max_length : 18;
  char_length = typeof char_length !== 'undefined' ? char_length : 15;

  // Some more code
}
```

## Reversed List of Elements

```
selectedItems = $(".selected").get().reverse();
```