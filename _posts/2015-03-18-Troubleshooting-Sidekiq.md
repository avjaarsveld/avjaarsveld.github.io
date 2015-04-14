---
title: Troubleshooting Sidekiq
layout: post
tags:
- sidekiq
- troubleshooting
- aws
- logs
---

## Starting Rake Sidekiq

Connect to AWS instance

Then...

```
sudo su deploy
cd tmp/pids/
ll
rm sidekiq.pid 
cd ..
..
bundle exec rake sidekiq:start
cd ..
cd log
ll
exit
```

## Checking Sidekiq Log (while running a job)

```
sudo su deploy
cd /srv/www/my/current
tail -f log/sidekiq.log
```

## Sidekiq won't stop or start

Try stop:

```
su su deploy
cd /srv/www/me/current
bundle exex rake sidekiq:stop
``

Try start:

```
su su deploy
cd /srv/www/me/current
bundle exex rake sidekiq:start
``

If those fail, try delete the sidekiq.pid and try start again:

```
rm -rf tmp/pids/sidekiq.pid 
bundle exec rake sidekiq:start
```
