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
because the programmer needs to work in a different way to most other editors/IDE's, it has a
relatively steep learning curve and requires the developer to spend a few weeks to learn how to use
it (that I've done) and more time to master it (that I have not found time for yet).

I therefore mainly use Jedit when programming, and use vim when jedit is not available
(say on someone else's computer) or when I need to quickly edit a file and I'm
already in the terminal.

I am currently in the process of setting up a new Ubuntu laptop, and thought now
would be a good time to make sure I am using the best editor/IDE for RoR programming.

## What others say

I started by having a look around for other's suggestions. As you'd expect there are
lots of people advocating their favourite, with at least ten front runners. For an
idea of what I mean, and/or a list of suggestions with screenshots and intro's, see
[here](http://askubuntu.com/questions/10998/what-developer-text-editors-are-available-for-ubuntu)

Redcar caught my eye as it seems to have lots of useful features (good auto-completion,
plug-ins, and all the others like syntax-highlighting and auto-indentation) and looks
easy enough to get into and learn. I also like the Textmate-like styling and way of doing things,
even though I've never actually used Textmate. It must be Ryan Bates' influence.

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

I love that you can quickly open files by pressing `Ctrl+T` and typing the first few letters of the
file name. I didn't love that the shortcut for deleting a line was `Ctrl+Shift+K` (K for Kill line).
So the 2nd thing I did was to change it to `Ctrl+Shift+D` (D for Delete line), as I'm used to
duplicating lines with `Ctrl+D` and deleting them with `Ctrl+Shift+D`. For the rest of the
shortcuts I'll try to learn them as is, as it'll mean I can switch to or borrow other computers
and environments without feeling lost.

To change shortcut keys, use the `Keyboard Shortcuts` tool in the `Help` menu, or edit
`key_bindings.yaml` which you can do in `Preferences` (`F2`).

The next thing I did was to set the `Margin Column` character count and to turn on `Show Margin`
and `Word Wrap`. I'm liking how redcar handles margins and auto-complete.

Finally I played around with auto-complete and suggestions in a ruby file, and tried out
block-selection to comment out multiple lines, or to edit multiple lines in other ways. To do
this, use `Ctrl+B` to toggle `block selection`, select the lines you want to edit and type away.

> **Note**

> Block selection does not work with word wrapping.

## That's all folks

Well, its Saturday night, so I think that's it for now. I'll see how I get on with Redcar when I 
do some real work next week...




