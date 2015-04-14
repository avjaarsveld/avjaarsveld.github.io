---
layout: post
title: Connect to an AWS instance from Ubuntu and copy the Postgres Database
tags:
- postgres
- pg
- postgresql
- psql
- database
- development
- ubuntu
- aws
- dump
---

## Connect to the instance, using the terminal

```
ssh ubuntu@public_ip
```

Given the instance's `public_ip` (e.g. `51.82.211.212`), which you can find listed
in the AWS console. At this point your public key should already be associated
with your AWS account, you can find more details here:
[help.github.com/articles/generating-ssh-keys/](https://help.github.com/articles/generating-ssh-keys/)

## Use pg_dump to create a copy of the Postgres database

```
pg_dump -Fc -h DB_Host -U root name > db.dump
```

`DB_Host` is listed in the RDS App detail's under "Environment Variables"
in the OpsWorks console. It should look something like
`name.c2bahyyit4qt.sa-north-1.rds.amazonaws.com`

## Enter the password

```
my_password
```

## Copy the file from the remote instance to local computer

On the local computer:

```
scp ubuntu@public_ip:db.dump ~/
```

## Import db dump into local db

```
bundle exec rake db:drop && rake db:create && pg_restore --verbose --clean --no-acl --no-owner -h localhost -U username -d db_name /home/me/db.dump
```

> Use `pg_restore --verbose --clean --no-acl --no-owner -h localhost -U username -d db_name /home/albert/db.dump`
> if restoring to a database that has just been created (drop and create not needed).

# Other Tasks - e.g. Launching the Console

## Switch to deply user

```
sudo su deploy
```

## Go to the app path

```
/srv/www/name/current
```

## Launch Console in Production Mode

```
bundle exec rails console -e production
```







