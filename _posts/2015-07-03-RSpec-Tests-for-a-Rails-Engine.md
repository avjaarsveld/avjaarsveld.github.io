---
layout: post
title: RSpec Tests for a Rails Engine
tags:
- engine
- tests
- rspec
---

Some notes on running RSpec tests for a Rails Engine.

> This sets up the test database, changes directory to the engine's directory and runs it's tests

```
bundle exec rake db:migrate
bundle exec rake db:test:prepare
bundle install
cd engines/live_class/
bundle exec rspec
```