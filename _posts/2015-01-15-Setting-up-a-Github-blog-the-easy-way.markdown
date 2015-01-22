---
layout: post
tags:
- blog
- jekyll
- redcarpet
- github pages
- markdown
- hosting
- CSS
- SASS
- Tagline
- Comments
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

### Post Tagline

I wanted to avoid excessivly long post titles, but I was creating a post that needed a long title. A
good solution is to break the title up into a title and tagline, and it turns out doing this with
Jekyll is really easy.

Simply add your tagline (or other custom variable) to the existing 
[front matter](http://jekyllrb.com/docs/frontmatter) like so:

```
---
layout: post
tagline: da bomb
tags:
- blog
- jekyll
---
```
Then reference the tagline like this: {% assign special = '{{ page.tagline }}' %} `{{ special }}`

Use this code in your `_layouts/post.html` file to display the tagline if it's defined:

``` html
{% raw %}
<h1 class="post-title">{{ page.title }}</h1>
{% if page.tagline %}
	<p>{{ page.tagline }}</p>
{% endif %}
{% endraw %}
```

### Comments

I chose to use [Disqus](https://disqus.com) for comments. As Github Pages serve static pages/sites
only, and comments are not static, you need a hosted comments service like Disqus.

To use Disqus with Jekyll, sign up on the Disqus site and select `Universal Code` when prompted for
the setup instructions you need. Then copy the code to where it's needed.

I created a `disqus.html` partial (in the `_includes` folder), which contains the code copied from
[disqus.com](https://disqus.com). I then include it where needed using
`{% raw %}{% include disqus.html %}{% endraw %}`

### About page<a name="about"></a>

Jekyll comes with a custom `about.md` page in the root. I added an `about me` link to the top of
every page by setting the `author: url:` to `http://avjaarsveld.github.io/about` (in `_config.yml`) 
and then creating
a `sitemenu` link that points to the `site.author.url` in the `_layouts/default.html` file, like so:

#### HTML:
``` html
{% raw %}
<div class="sitemenu right">
	<small>
		<a href="{{ site.author.url }}"
		  title="About {{ site.author.name }}">about me</a>
	</small>
</div>
{% endraw %}
```

#### CSS:
``` css
.sitemenu a {
	color: #c0c0c0;
	margin-left: 16px;
}
```

### Index of Posts

I added an `index of posts` link to the top of every page in the same way that I added the `about me`
link (as mentioned [above](#about)):

#### HTML:
``` html
{% raw %}
<div class="sitemenu right">
	<small>
		<a href="/post-index" title="Index of posts">
		  index of posts
		</a>
		<a href="{{ site.author.url }}"
		  title="About {{ site.author.name }}">about me</a>
	</small>
</div>
{% endraw %}
```

I then added an `post-index.html` page to the root, and used similar html to the `index.html` page
to show a list of posts, but with the first 30 words shown (html stripped) rather than the whole post.
A `read more...` link is also used.

#### post-index.html HTML:
``` html
{% raw %}
<div class="posts">
  <h1>{{ page.title }}</h1>
  <hr />
  {% for post in site.posts %}
  <article class="post">
    <h2 class="post-title">
      <a href="{{ post.url }}">
        {{ post.title }}
      </a>
    </h2>
    {% if post.tagline %}
      <p class="tagline">{{ post.tagline }}</p>
    {% endif %}

    <time datetime="{{ post.date | date_to_xmlschema }}" class="post-date">
      {{ post.date | date_to_string }}
    </time>
    {{ post.content | strip_html | truncatewords:30 }}<br />
    <small>
      <a class="right" href="{{ post.url }}">Read more...</a>
    </small>
    <hr />
  </article>
  {% endfor %}
</div>
{% endraw %}
```
