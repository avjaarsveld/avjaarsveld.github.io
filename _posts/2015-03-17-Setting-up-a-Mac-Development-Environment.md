---
layout: post
title: Setting up a RVM, Ruby, Rails, Bundle, Git on a Macbook
tagline: Not tested yet - may be incomplete
tags:
- development
- ruby
- rails
- rvm
- bundler
- bundle
- git
- mac
- macbook
---

I've got another new laptop. This time it's a Macbook Pro, so I thought I'd
document what I do to set up my Mac development environment, to make it easier 
for me next time, and to help you out...

> I created these notes while doing the setup, but I have not yet had a chance to review or test
> them (I'll do that the next time I set up a Mac development computer). In the mean time,
> please excuse any errors or omissions (or better yet, let me know in the comments)

## 1. Installing the basics

The OS was already installed, along with the usual Mac goodies. You may need to install
git (see below).

## 3. SSH Keys are required to connect to github

This is to-do.

## 5. Install RVM (and Rails etc)

If, like me, you have multiple projects with different gems, using different version of Rails,
you'll need [RVM](https://rvm.io/). I installed Rails via RVM (after installing RVM) and installed
MySQL separately. This is how:

> **Note:**
> Follow the latests instructions on
> [railsapps.github.io](http://railsapps.github.io/installrubyonrails-mac.html) for
> Mac OS X version 10.10 or
> [moncefbelyamani.com](http://www.moncefbelyamani.com/how-to-install-xcode-homebrew-git-rvm-ruby-on-mac/)
> for Mac OS X version 10.9 (and older)
> and/or [rvm.io/rvm/install](https://rvm.io/rvm/install)

> If you have Ruby already installed, you do not need to remove it, RVM will leave it untouched.

## 1. Install Xcode Command Line Tools

First check that it is not already installed. `xcode-select -p` should return `/Library/Developer/CommandLineTools`
and `gcc --version` should not return an error message.

If not installed, install using:

```
xcode-select --install
```

## 2. Setup git

> Git is automatically installed as part of the Xcode Command Line Tools (see above).

Check if git has already been set up using `git config -l --global`.

if nessesary, add your username and email for git:

```
git config --global user.name "Peter Pan"
git config --global user.email "peter@neverland.com"
```

## 4. Clone a repo into a new folder

```
git clone git@github.com:pirate_bay/pirate_ship.github.io.git pirate_ship
git clone https://avjaarsveld@bitbucket.org/neverland_resort/atm_system.git atm_system
```

## 1. Install Homebrew

```
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

> Check that Homebrew is installed/setup correctly using `brew doctor` which
> should return `Your system is ready to brew.`

## 5. Intall RVM

```
\curl -sSL https://get.rvm.io | bash -s stable --ruby
```

Run `source /Users/me/.rvm/scripts/rvm` in all your open shell windows as instructed

Test RVM with `type rvm | head -1` which should return `rvm is a function`

### Optionally Install a version of Ruby

```
rvm install 1.9.3
```

The above installs a specific version. `rvm install 1.8.7-p374` installs a specific version and
patchlevel. `rvm install ruby --latest` installs the latest version.

### Create a Gemset for installed Ruby version

> List gemsets with `rvm gemset list`

This is also to-do.

## Install Bundler

> Bundler is installed with Ruby or RVM

Used bundler to install Rails and other gems using `bundle install`


### Install gems listed in Gemfile:

```
bundle install
```

> This failed as `capybara-webkit` failed to install. I fixed this by instaling Qt first
> `brew install qt`.

> `bundle install` failed again as pg failed to install with "Can't find the libpq-fe.h header".
> This was because PostgreSQL was not installed on the machine yet, which I fixed with
> `brew install postgresql`

> Failed again as the `rmagick` gem failed to install. This was because ImageMagic was
> not installed on the system and was fixed with `brew install imagemagick`

### Check bundler is working:

`bundle -v` or `bundle exec rails s` or `bundle exec jekyll serve`

## Setting up Postgres

PostgreSQL was set up (see above) with `brew install postgresql`. This is what I did to
get it set up.

To have launchd start postgresql at login:

```
ln -sfv /usr/local/opt/postgresql/*.plist ~Library/LaunchAgents
```

Then to load postgresql now:

```
launchctl load ~/Library/LaunchAgents/homebrew.mxcl.postgresql.plist
```

Install Instrumentation:

```
psql postgres -c 'CREATE EXTENSION "adminpack";'
```

Create user:

```
psql postgres -c "CREATE USER username WITH PASSWORD 'password';"
```

Create Database:

```
psql postgres -c "CREATE DATABASE db_name WITH OWNER username;"
```

Grant privileges:

```
psql postgres -c "GRANT ALL PRIVILEGES ON DATABASE db_name TO username;"
```

## Redis

When trying to launch the rails console/server I got a Sidkiq/Redis error as
the machine did not have Redis installed. This was fixed with:

```
brew install redis
redis-server &
```

