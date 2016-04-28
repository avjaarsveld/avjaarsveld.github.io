---
layout: post
title: Setting up a RVM, Ruby, Rails, Bundle, Git and Ubuntu Development Environment
tagline: Not tested yet - may be incomplete
tags:
- development
- ruby
- rails
- rvm
- bundler
- bundle
- git
- ubuntu
---

I've got a new laptop, so I thought I'd share what I do to set up my development
environment, to make it easier for me next time, and to help you out...

> I created these notes while doing the setup, but I have not yet had a chance to review or test
> them (I'll do that the next time I set up an Ubuntu development computer). In the mean time,
> please excuse any errors or omissions (or better yet, let me know in the comments)

## 1. Install Ubuntu

I chose Ubuntu 14.04 LTS this time.

## 2. Install git

```
sudo apt-get install git
```

Add username + email for git, as prompted the first time you try to use git:

```
git config --global user.name "Peter Pan"
git config --global user.email "peter@neverland.com"
```

## 3. SSH Keys are required to connect to github

Follow instructions here to generate and add a key: [help.github.com/articles/generating-ssh-keys/](https://help.github.com/articles/generating-ssh-keys/)

## 4. Clone a repo into a new folder

```
git clone git@github.com:avjaarsveld/avjaarsveld.github.io.git avjaarsveld.github.io
```

## 5. Install Bundler (and Rails, MySQL, etc)

To get Rails (and MySQL) installed you could install Bundler and then used it to install Rails and
other gems using `bundle install`, as shown [below](#no-rvm). This works great if you only have one Rails
project on your computer (or if all your Rails projects use exactly the same gem set.

If, like me, you have multiple projects with different gems, using different version of Rails,
you'll need [RVM](https://rvm.io/). I installed Rails via RVM (after installing RVM) and installed
MySQL separately. This is how:

### Install RVM

> Follow the latests instructions on
> [railsapps.github.io](http://railsapps.github.io/installrubyonrails-ubuntu.html)
> and/or [rvm.io/rvm/install](https://rvm.io/rvm/install)

> If you have Ruby already installed, you do not need to remove it, RVM will leave it untouched.

```
sudo apt-get update
```

```
sudo apt-get install curl
```

```
gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
```

> That last command seemed to fail with the following error, but I was able to continue with the
> installation:

> ```
> gpg: requesting key D39DC0E3 from hkp server keys.gnupg.net
> gpg: keyserver timed out
> gpg: keyserver receive failed: keyserver error
> ```

```
\curl -sSL https://get.rvm.io | bash
```

```
source /home/albert/.rvm/scripts/rvm
```

### Install a version of Ruby

```
rvm install 1.9.3
```

The above installs a specific version. `rvm install 1.8.7-p374` installs a specific version and
patchlevel. `rvm install ruby --latest` installs the latest version.

### Create a Gemset for installed Ruby version

```
rvm use 1.8.7-p374@my-project --create
```

> See [rvm.io/gemsets/creating](https://rvm.io/gemsets/creating) for more options.

```
rvm --ruby-version use 2.2.0
# OR rvm --ruby-version use 2.0.0@my-project
```

> Optionally add `rvm 1.8.7-p374@my-project` to your .rvmrc file instead of using a `.ruby-version`
> and `.ruby-gemset` file as shown above. See
> [rvm.io/workflow/projects](https://rvm.io/workflow/projects) for more details.

## Install Bundler  (and Rails, MySQL, etc)<a name="no-rvm"></a>

Install Bundler and then used it to install Rails and other gems using `bundle install` (this is
not nessesary if you've already installed RVM, etc as shown above)

```
sudo apt-get install bundler
```

### Install gems listed in Gemfile:

```
bundle install
```

### Check bundler is working:

`bundle -v` or `bundle exec rails s` or `bundle exec jekyll serve`

## More Customization

### Git Aliases

Add a simple alias (and create the .gitconfig file if it's not already created) with `git config --global alias.st status`

Edit .gitconfig and add any other aliases you'd like to use, like:

```
st = status
l = log
uncommit = !git reset --soft 'HEAD^' && echo '' && git status
sreset = !git uncommit

# Add All and Commit
aac = !echo "Enter commit message:" && read MSG && echo "" && echo "Status before chagnes:" && echo "======================" && git status && echo "" && echo "Adding all..." && echo "=============" && git add . && echo "" && echo "Committing..." && echo "=============" && git commit -m \"$MSG\" && echo "" && echo "New status:" && echo "===========" && git status

# Commit with bumped Version number
cv = !git commit -m \"Bumped to version $(head -n 1 VERSION)\"

# Add All and Commit with bumpted Version number
aacv = !echo "Status before chagnes:" && echo "======================" && git status && echo "" && echo "Adding all..." && echo "=============" && git add . && echo "" && echo "Committing..." && echo "=============" && git commit -m \"Bumped to version $(head -n 1 VERSION)\" && echo "" && echo "New status:" && echo "===========" && git status
```

See [this article](http://haacked.com/archive/2014/07/28/github-flow-aliases/) for some good advice RE Git Aliases.

### ZSH (Command Alisases)

After installing ZSH, you may want to add some aliases here too, like `alias edit="subl --wait --new-window"`

Open .zshrc (`subl ~/.zshrc`), add the above mentioned alias to the alias section, save, close and run `. ~/.zshrc` to update the terminal. Now you can use `edit ~/.gitconfig` etc to open files or folders in Sublime.