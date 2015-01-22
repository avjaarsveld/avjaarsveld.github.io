---
layout: post
---

## My first post.. but Why?

I thought it's about time that I organise and back up my notes, and while I'm at it I might as
well make them available to others. So here goes...

## Which?

Firstly I needed to decide *which* tools to use to publish the blog. I already use github every day at
work, and I knew they had this nifty (yes Fiona, I said "nifty",
I admit it, I'm a geek) GitHub Pages feature that would allow me to easily publish a static site at
no cost (and easily update it). So using Github Pages was an easy choice. If you use Bitbucket, they
offer something similar, but as I already use Gitbub for work, Github Pages was the way to go for me.

## How?

[pages.github.co](http://pages.github.com) is a good introduction with quick setup instructions.

If you want to use [markdown](https://daringfireball.net/projects/markdown/syntax) or
[textile](http://txstyle.org) syntax for pretty headings and hyperlinks and code,
you'll want to use Jekyll.

> **BTW**

> If you want your code snippets syntax highlited like this

> ``` ruby
def me
  puts "ok" if sound
end
```

> you'll need to use [redcarpet](https://github.com/blog/832). More on that [later](#redcarpet).

[help.github.com/articles/using-jekyll-with-pages](https://help.github.com/articles/using-jekyll-with-pages)
will get you started with Jekyll. Assuming you already use Ruby abd Bundler, simply add
`gem 'github-pages'` to your `Gemfile` and run `bundle install` to install it.

Use `bundle exec jekyll serve` to serve your pages locally, accessible at [http://localhost:4000](http://localhost:4000)

Find out more about Jekyll [usage](http://jekyllrb.com/docs/usage) and [configuration](http://jekyllrb.com/docs/configuration)
by looking at the **Getting Started** section of the [Jekyll Github page](https://github.com/jekyll/jekyll)

### Styling

To make your blog easier and more enjoyable to read, you need some styling. You can define the CSS
(or SASS) youself and make the site look exactly the way you want, or you can use template styling (and
optionally edit the CSS to get exactly what you want, if that's important to you).

I wanted a clean, neat, easy to read, no clutter blog. I found [Poole](http://demo.getpoole.com).
Installing it is easy, see the [Poole Github page](https://github.com/poole/poole/find/master)
for instructions.

Styling wise, Pool was pretty much exactly what I wanted, but I did tweek some headings and the odd colour
by editing the CSS files (in `public/css/`) and I may convert these to SASS in future [# TODO]. I
am still wondering whether it's obvious enough that *Styling* is a h3 and not a h2..?

> **Note**

> Poole does more than give you some pretty nice CSS for Jekyll.

> Change the default site name and author in `_config.yml`.

### Syntax Highliting<a name="redcarpet"></a>

Use [redcarpet](https://github.com/blog/832) to do this the Github way. Simply add
`markdown: redcarpet` to your `_config.yml` file (or replace any existing `markdown: something_else` line).

You can then type in something like:

<pre>
``` ruby
def me
  puts "ok" if sound
end
```
</pre>

to get:

``` ruby
def me
  puts "ok" if sound
end
```
