---
layout: post
tags:
- rails
- generate
- migrations
- development
---

# Rails Generate

### References

Add a `charity_id` index to the `Candidate` model (Candidate belongs to Charity)

```
bundle exec rails generate migration add_charity_to_candidate charity:references
```

```
bundle exec rails generate scaffold Branch charity:references name:string description:string url:string country:string country_region:string city:string phone_number:string
```

### Scaffold with Polymorphic

```
rails generate scaffold need_tag name:string tagable:references{polymorphic}
```

# Setup Rails with Tests

I don't need to do this very often, so when I do there is always something I need to look up. So time to make some notes...

```
cd ~/projects/
```

I already have rails installed, if you don't you'll need to get it installed. There are some notes on this site that cover getting an Ubuntu or Mac set up that may help.

```
rails new example
```

```
cd example
```

Next you need to add `rspec-rails` to your `Gemfile` (in the `:development` and `:test` groups). You can do this the easy but fractionally more laborious way by adding `gem 'rspec-rails'` to your `Gemfile`, <b>or</b> by using this super-cool line (courtesy of the relishapp.com help files): `echo "gem 'rspec-rails', :group => [:development, :test]" >> Gemfile`

> Manually adding `gem 'rspec-rails'` to your `Gemfile` will result in a slightly neater `Gemfile`

```
bundle
```

```
rails generate rspec:install
```

Now to add something to your new site to test. Lets say, for example, you want to keep a record of given/long URL's and corresponding generated/short URL's, you may do something like `rails generate scaffold Url long_url:string short_url:string`.

> I prefer HAML to ERB view files, so I did this (skip these steps if you are happy with ERB)

> If you ran the rails generate above you can undo it like this `rails destroy scaffold Url long_url:string short_url:string`

> Add `gem 'haml'` and `gem 'haml-rails'` to your `Gemfile`

> `bundle`

> `rails generate scaffold Url long_url:string short_url:string`

> You get nice HAML view files

```
rake db:migrate && rake db:test:prepare
```

```
rspec
```

The tests should pass, with some pending tests. Congratulations, you have now set up rails with tests and can go ahead and get all tests working and/or add new functionality (as shown below)

## Get the skipped/pending tests working

### Valid URLs

Replace `skip("Add a hash of attributes valid for your model")` with something like `{long_url: 'http://www.mysite.com/some-kind-of-page.html', short_url: 'http://me.co/hrt12'}` in `urls_controller_spec.rb` to get most of the pending tests passing (as you can see by running `rspec` again).

### Invalid URLs

Replace `skip("Add a hash of attributes invalid for your model")` with something like `{long_urls: 'not a valid long url', short_url: 'not a valid short url'}` and run `rspec` again.

We get some errors. The top errors can be fixed by adding validation to the `Url` model. We should not allow invalid URL's, so lets try `validates_format_of :long_url, :short_url, :with => URI::regexp(%w(http https))`.

Running `rspec` shows fewer erros, all of which are from view specs/tests. Replace entries like `:long_url => "MyString"` (which are not valid according to the validation we just added) with something like `:long_url => 'http://www.mysite.com/some-kind-of-page.html'`.

Do `rspec` again and all tests are passing again, but we still have 3 pending. One of them is easily fixed following the same route as above and the last two are for UrlsHelper which is not yet implemented.

Congratulations, you have now set up rails with working tests and can go ahead and add new functionality.

## Add new functionality

I'd like to generate short URL's based on the user supplied long URL's (rather than asking the user to supply both). To do this we first need to update our tests... (I've run out of time for now, so the rest of these notes are pending)
