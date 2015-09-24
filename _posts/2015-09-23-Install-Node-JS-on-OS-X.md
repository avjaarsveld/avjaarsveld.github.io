---
layout: post
tags:
- nodejs
- install
- development
title: Install Node JS and Bower on OS X
---

## Node JS and NPS

Installing node.js on OS X is really simple, this is how

1. Go to [nodejs.org](https://nodejs.org/) and click to download for your OS (e.g. `Download for OS X (64)`)

2. Double click on on the downloaded package (e.g. `node-v4.1.1.pkg`)

3. Follow the instructions to install, as per the summary you get on the last screen, check that /usr/local/bin is in your $PATH:

    3.1. In the terminal type `echo $PATH`, `/usr/local/bin` should be shown in the `:` seperated string

4. Check that it works:

    4.1. In the terminal type `node` to launch the node console

    4.2. `console.log('something')` should return `something undefined`

    4.3. `CTRL + C` twice or `process.exit()` to exit

## Bower

Installing Bower on OS X is really simple, this is how

1. Install node.js and nps (and git) - see above

2. Install [bower](http://bower.io/): `sudo npm install -g bower`

3. Install Packages: `bower install`