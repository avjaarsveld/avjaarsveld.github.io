---
layout: post
title: Using Postgres for the First Time (instead of MySQL)
tagline: Setting Up Postgres
tags:
- postgres
- pg
- postgresql
- psql
- database
- development
- ruby
- gems
---

I've been asked to look at a project that uses Postgres. This is what I needed to do to get
it running in a development environment. The different/interesting bits are in the
[Setup the Database](#db) section, below.

## 1. Clone Repo

```
git clone https://me@bitbucket.org/some/repo.git myfolder
```

## 2. Set Ruby

```
rvm use 2.1.5
```

## 3. Install Gems (including pg)

```
bundle install
```

> `bundle install` may be all you need if all the right gems are listed in the `Gemfile`

This failed for me, as `pg` failed to install. To fix this, I installed `libpq-dev` first:

```
sudo apt-get install libpq-dev
```

Then checked that the `pg` gem (the version listed in the `Gemfile`) installed ok:

```
gem install pg -v '0.18.0`
```

This worked ok, so I tried `bundle install` again, which worked this time.

## 4. Setup the Datatbase <a name='db'></a>

> See: [stackoverflow.com/a/19829605/1887925](http://stackoverflow.com/a/19829605/1887925)

### Install Postgresql

```
sudo apt-get install postgresql
```

### Setup a Postgres DB User and create the Database

```
which psql
sudo su - postgres
psql
```

```
CREATE USER username WITH PASSWORD 'password';
CREATE DATABASE db_name WITH OWNER username;
GRANT ALL PRIVILEGES ON DATABASE db_name TO username;
```

> `\q` <enter> to exit from the PostgreSQL command line utility (psql),
> then `exit` to exit sudo su as normal

### Run Migrations to complete DB setup

```
bundle exec rake db:migrate
```
