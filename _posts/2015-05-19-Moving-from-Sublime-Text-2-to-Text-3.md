---
layout: post
tags:
- Sublime
- Text 2
- Text 3
- Theme
- Colour Theme
- Linter
---

I've recently "upgraded" from Sublime Text 2 to Sublime Text 3. Here are some notes about how to get Text 3 setup
for better productivity and to keep my Colour Theme.

## Installing Add-Ons (Packages)


E.g:

1. `CMD + Shift + P`
2. Package Control: Install Package
3. `GitGutter`

Packages installed: GitGutter, BetterCOffeescript, [SublimeLinter](https://www.youtube.com/watch?v=u6fvJRao-E4), [SidebarEnhancements](https://www.youtube.com/watch?v=Cat734Z-AhA), AllAutocomplete, [BracketHighlighter](https://www.youtube.com/watch?v=Cc-8W7qBu9Q)

> For SublimeLinter: `CMD + P` `Toggle Linter` to enable/disable linters.

## Copying Colour Theme

This is how I moved my colour theme from Sublime Text 2 to Text 3. It works, but is probably not the best way to do it. If you know of a better way, please leave a comment.

```
cd /Applications/Sublime\ Text\ 3.app/Contents/MacOS/Packages/
cp Color\ Scheme\ -\ Default.sublime-package ~/Documents/
cd ~/Documents/
unzip Color\ Scheme\ -\ Default.sublime-package -d temp
cd /Users/me_username/Library/Application\ Support/Sublime\ Text\ 2/Packages/Color\ Scheme\ -\ Default/
```

Make your edits. In my case I copied over my `Monokai Faded` colour theme file as shown above.

```
cp Monokai\ Faded.tmTheme ~/Documents/temp
cd ~/Documents/temp
```

Compress all files in folder to a new archive called `Color Scheme - Default.sublime-package`

```
cp ~/Documents/temp/Color\ Scheme\ -\ Default.sublime-package /Applications/Sublime\ Text\ 3.app/Contents/MacOS/Packages/
```