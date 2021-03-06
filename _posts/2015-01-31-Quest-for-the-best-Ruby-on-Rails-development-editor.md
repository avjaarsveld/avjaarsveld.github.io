---
layout: post
tagline: ...that is also easy to use and learn
tags:
- development
- ruby
- editor
- redcar
---

Vim is powerful, popular and helps lots of developers to be more efficient programmers. However,
because Vim forces you to work in a different way to most other editors/IDE's, it has a
relatively steep learning curve and requires the developer to spend a few weeks to learn how to use
it (that I've done) and more time to master it (that I have not found time for yet).

I therefore mainly use Jedit when programming, and use Vim when jedit is not available
(say on someone else's computer) or when I need to quickly edit a file and I'm
already in the terminal.

I am currently in the process of setting up a new Ubuntu laptop, and thought now
would be a good time to make sure I am using the best editor/IDE for RoR programming.

> Since writing this post I have switched to mainling using Sublime Textmate 2 on a Macbook, and
> occasionally using Sublime on Ubuntu, and rarely using Vim and hardly ever using Redcar and Jedit.
> I'd say that untill Redcar becomes better supported Sublime is the way to go.

## What others say

I started by having a look around for other's suggestions. As you'd expect there are
lots of people advocating their favourite, with at least ten front runners. For an
idea of what I mean, and/or a list of suggestions with screenshots and intro's, see
[here](http://askubuntu.com/questions/10998/what-developer-text-editors-are-available-for-ubuntu)

Redcar caught my eye as it seems to have lots of useful features (good auto-completion,
plug-ins, and all the others like syntax-highlighting and auto-indentation) and looks
easy enough to get into and learn. I also like the Textmate-like styling and way of doing things,
even though I've never actually used Textmate. It must be Ryan Bates' influence.

> Since writing this post I have started using Sublime Text 2 more and Redcar less, mainly
> because Redcar is not yet a 100% finished project making Sublime Text slighlty more
> conducive to quick and painless development.

## Install the Redcar Editor

As mentioned [here](http://superuser.com/questions/303345/redcar-install-through-rvm) and
in the [installation wiki](https://github.com/redcar/redcar/wiki/installation) you'll need
java to run/install redcar as its a JRuby application.

```
sudo apt-get install openjdk-6-jre
```

Then to install it, all I had to do was:

```
sudo gem install redcar
```

and then:

```
redcar install
```

Redcar installed and opened. If it does not open after installing, try `redcar` in the terminal.

## Using Redcar for the first time

Launch Redcar (see above), then use `Open a Directory` (see the `File` menu or use `Ctrl+Shift+O`)
to open your project's folder. The folder tree should open, if it does not check this
behaviour is set in `Preferences` (`F2`).

From there you can open files and edit them. I have never used Textmate, but if you have
you should find that everything works as you're used to. That's because Redcar is
based on Textmate (it's Textmate for Linux).

### Shortcuts

I love that you can quickly open files by pressing `Ctrl+T` and typing the first few letters of the
file name. I didn't love that the shortcut for deleting a line was `Ctrl+Shift+K` (K for Kill line).
So the 2nd thing I did was to change it to `Ctrl+Shift+D` (D for Delete line), as I'm used to
duplicating lines with `Ctrl+D` and deleting them with `Ctrl+Shift+D`. For the rest of the
shortcuts I'll try to learn them as is, as it'll mean I can switch to or borrow other computers
and environments without feeling lost.

To change shortcut keys, use the `Keyboard Shortcuts` tool in the `Help` menu, or edit
`key_bindings.yaml` which you can do in `Preferences` (`F2`).

> **Note**

> `Ctrl X` (cut) will delete a line if nothing is selected. The kill (delete) shortut is useful when
> deleting multiple lines (select text across multiple lines and execulte this command).

### Word Wrap, Margin, etc

The next thing I did was to set the `Margin Column` character count and to turn on `Show Margin`
and `Word Wrap`. I'm liking how redcar handles margins and auto-complete, but after trying out
`Word Wrap` I find that more often than not I do not use it. Luckily Redcar remembers this setting
for each project/directory you open, so you can set this up per project (e.g. based on the type of
project).

### Edit multiple lines simultaniously

I played around with auto-complete and suggestions in a ruby file, and tried out
block-selection to comment out multiple lines, or to edit multiple lines in other ways. To do
this, use `Ctrl+B` to toggle `block selection`, select the lines you want to edit and type away.

> **Note**

> Block selection does not work with word wrapping.

### .gitignore

I needed to add `.redcar` to my `.gitignore` file. Better yet, add it to your global gitignore file,
like so:

Create the global gitignore file, in this example called `gitignore_global`

```
git config --global core.excludesfile '~/.gitignore_global'
```

Then edit the file, and include what you want to ignore, for example:

```
*~
.redcar
```
