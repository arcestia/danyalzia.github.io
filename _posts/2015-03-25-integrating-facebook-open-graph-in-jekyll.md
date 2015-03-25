---
layout: post
title: Integrating Open Graph Meta Tags In Jekyll
thumbnail: /media/images/ogp-jekyll.png
---
![Integrating Facebook Open Graph in Jekyll]({{baseurl}}/media/images/ogp-jekyll.png)
<span class="firstcharacter">I</span> was in the process to share my blog posts on Facebook through [AddThis](http://www.addthis.com/) sharing buttons which is below each of my blog posts, but then it turned out that the links don't show the thumbnails on it, nor title and description, just *danyalzia.com* as a title and description of the link. Instead of panicking about it, I googled the problem (that's what genius people do!).

Google told me that there is a protocol, namely, [Open Graph protocol](http://ogp.me/), which Facebook and other social media platforms use to crawl objects on a page. It helps webmasters/bloggers in optimising their blog/site when sharing on social media networks, resulting in the increase of [Click-through rate](http://en.wikipedia.org/wiki/Click-through_rate) due to proper appearance of objects (title, images, etc.) in links. It provides HTML snippets which you can put in your website's HTML head to give it some attributes.

Many blogging platforms, such as, WordPress, Blogger, etc. already provide *Open Graph meta tags* in their themes, but unfortunately, Jekyll (at least the [lanyon](https://github.com/poole/lanyon) theme which I use for this blog) don't support *Open Graph meta tags*, so I had to manually put them in my source trunk.

Through *Open Graph meta tags*, I can control over how my content is displayed when shared via Facebook. In this blog post, I am going to show you how you can add Open Graph meta tags in your Jekyll site.

### 1) Visiting Facebook Object Debugger

You need to visit the Facebook's [Object Debugger](https://developers.facebook.com/tools/debug/og/object) page. You will see that you can add your link to your blog post to scrap the information. Just add your link in the box and click on "Fetch new scrape information".

![]({{baseurl}}/media/images/Facebook-object-debugger.png)

If you are lucky enough, then Facebook will automatically put *Open Graph meta tags* in your blog post, such as, *og:title*, *og:description*, *og:image*, etc. But at most times, Facebook finds it hard to crawl such information and you end up sharing your post without proper thumbnail, title, description, etc.

![]({{baseurl}}/media/images/Facebook-object-debugger-link.png)

### 2) Add the Open Graph Snippets

If you are using Jekyll like me for your blogging/website needs, then you need to find `head.hml` in your `_includes` folder and add the code snippets of *Open Graph meta tags* of your choice under `<head>`. Basic meta tags looks like the following:

{% highlight HTML %}
<meta content="title" property="og:title">
<meta content="type" property="og:type">
<meta content="image" property="og:image">
<meta content="url" property="og:url">
{% endhighlight %}

You can manually add your title, type (website, article, etc.), image and url, but we can use liquid syntax to automatically scrap the objects from our Jekyll blog. My complete code looks like the following:

{% highlight HTML %}{% raw %}

<meta property="og:title" content="{% if page.title %}{{ page.title }}{% else %}{{ site.title }}{% endif %}">

<meta property="og:type" content="{% if page.thumbnail %}article{% else %}website{% endif %}">

<meta property="og:url" content="{{ page.url | replace:'index.html','' | prepend: site.baseurl | prepend: site.url }}">

<meta property="og:image" content="{% if page.thumbnail %}{{ page.thumbnail | prepend: site.baseurl | prepend: site.url }}{% else %}{{ {{baseurl}}/avatar | prepend: site.baseurl | prepend: site.url }}{% endif %}">

<meta property="og:description" content="{% if page.description %}{{ page.description | strip_html | strip_newlines | truncate: 160 }}{% endif %}">

<meta property="og:site_name" content="{{ site.title }}">

<meta property="og:locale" content="{{ site.locale }}">

{% if page.date %}
  <meta property="article:published_time" content="{{ page.date | date_to_xmlschema }}">
  <meta property="article:author" content="{{ site.fb_admins }}">
  {% for post in site.related_posts limit:3 %}
    <meta property="og:see_also" content="{{ post.url | replace:'index.html','' | prepend: site.baseurl | prepend: site.url }}">
  {% endfor %}
{% endif %}

<meta property="fb:admins" content="{{ site.fb_admins }}">
<meta property="fb:app_id" content="{{ site.fb_appid }}">

{% endraw %}
{% endhighlight %}

I add `thumbnail` in blog posts, so if there is no `thumbnail`, then the page type is `website`, otherwise it's an `article`. If it's a website, then the thumbnail on the links will be my avatar.

### 3) Add the relevent info in _config.yml YAML Front Matter

You need to add the variables (if any) that you've used in the meta tags. My `_config.yml` have the related variables for few properties:

```
fb_admins:			http://facebook.com/danyal.zia.k
fb_appid:			337414769782635
avatar:				media/images/danyal-zia-avatar.png
```

### 4) Validate your links

Now once you have added the code in your `head.html`, you need to update the source trunk of your Jekyll blog and validate your [url](https://developers.facebook.com/tools/debug/).

![]({{baseurl}}/media/images/Facebook-object-debugger-sample-link.png)

## Conclusion

In this blog post, I have provided the information on Open Graph protocol and how it can be used to optimise the sharing of your blog posts. If you have any questions, then ask in the comments section below. Why not follow me on [Twitter](http://twitter.com/danyalzk) and [Facebook](http://facebook.com/danyal.zia.k)?
