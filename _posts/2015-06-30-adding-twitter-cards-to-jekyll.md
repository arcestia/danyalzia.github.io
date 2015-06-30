---
layout: post
title: Adding Twitter Cards To Jekyll
description: Learn the process to add Twitter Cards in your Jekyll website
thumbnail: /media/images/twitter-jekyll.png
---
![Adding Twitter Cards To Jekyll]({{baseurl}}/media/images/twitter-jekyll.png)

<span class="firstcharacter">I</span>n the past, I've discussed about the Open Graph and its [integration with Jekyll](http://danyalzia.com/2015/03/25/integrating-facebook-open-graph-in-jekyll/), where Open Graph tags are used in the HTML to control the content display while sharing on social media networks, particularly Facebook. The tags work pretty well on those sites which natively support Open Graph, such as, Facebook, Google+, etc., however, Twitter doesn't support Open Graph tags to control the content's display.

Worry not, as Twitter provide [Twitter Cards](https://dev.twitter.com/cards/overview) with its own tags to support the content display control of your blog posts which you share on Twitter. What it actually does, is that it can provide a title, thumbnail and description of your blog post just below your tweet which you shared on your Twitter profile. This results in a higher probability of [Click-through rate](http://en.wikipedia.org/wiki/Click-through_rate), as such links look cool and encourages your audience to click on your links. By simply adding a few lines of HTML to your webpage, the users who Tweet links to your content will have a “Card” added to the Tweet that’s visible to all of their followers.

Jekyll, as we have seen before, supports pretty much anything one can do with HTML/CSS/Javascript. With the inclusion of a short code snippet in your Jekyll repository, you can easily integrate Twitter Cards to your Jekyll site. Although, Twitter Cards come in [4 flavours](https://dev.twitter.com/cards/types) (Summary Card, Summary Card With Large Image, App Card, Player Card), I chose the [Summary Card](https://dev.twitter.com/cards/types/summary) because of its simplicity. Following is the process of adding the Summary Card to your Jekyll site:

### 1) Understand the structure of your site

Summary Card allows the users to preview the site content within a tweet. In order for Twitter Cards to support your site, you must have three parameters in your site: title, description and image. Twitter Cards will use that information to create a unique card for your links. **title**, **description** and **url** can be either added in `_config.yml` or in the YAML Front Matter block of your blog posts. The relevant parts in my `_config.yml` looks like following:

```
title:               Danyal Zia
description:         "Danyal Zia's thoughts on software development, personal development and writing."
url:                 http://danyalzia.com
avatar:				 media/images/danyal-zia-avatar.png
```

Relevant parts in the YAML Front Matter block of my blog posts:

```
title: 5 ways to motivate yourself
description: The guide to develop your self-motivation
thumbnail: /media/images/motivation.jpg
```

### 2) Add the Twitter Cards snippet

As you are using Jekyll like me for your blogging/website needs, the simplest way to add Twitter Cards to your site is to find `head.hml` in your `_includes` folder and add the code snippets of *Twitter Summary Cards* under `<head>`. The basic HTML meta tags that Twitter provides looks like the following:

{% highlight HTML %}{% raw %}
<meta name="twitter:card" content="summary" />
<meta name="twitter:site" content="@flickr" />
<meta name="twitter:title" content="Small Island Developing States Photo Submission" />
<meta name="twitter:description" content="View the album on Flickr." />
<meta name="twitter:image" content="https://farm6.staticflickr.com/5510/14338202952_93595258ff_z.jpg" />
{% endraw %}
{% endhighlight %}

You can manually add your title, description and image, but we can use liquid syntax to automatically scrap the objects from our Jekyll blog. My complete code looks like the following:

{% highlight HTML %}{% raw %}
<meta name="twitter:card" content="summary">
<meta name="twitter:site" content="@site_username">
<meta name="twitter:creator" content="@creator_username">
{% if page.title %}
  <meta name="twitter:title" content="{{ page.title }}">
{% else %}
  <meta name="twitter:title" content="{{ site.title }}">
{% endif %}
{% if page.url %}
  <meta name="twitter:url" content="{{ site.url }}{{ page.url }}">
{% endif %}
{% if page.description %}
  <meta name="twitter:description" content="{{ page.description }}">
{% else %}
  <meta name="twitter:description" content="{{ site.description }}">
{% endif %}
{% if page.thumbnail %}
  <meta name="twitter:image:src" content="{{ site.url }}/media/images/{{ page.thumbnail }}">
{% else %}
  <meta name="twitter:image:src" content="{{ site.url }}/media/images/danyal-zia-avatar.png">
{% endif %}
{% endraw %}
{% endhighlight %}

Here, I chose Twitter handle for both **site** and **creator**. If it's a blog post, then the **title** would be the name of the blog post, otherwise it will be the name of the blog (i.e., Danyal Zia). Similar logic has been applied for **url**, **description** and **image**.

Instead of adding the code in `head.html`, I created a new file `twittercards.html`, copied the code in it, and included in my `head.html`.

{% highlight HTML %}{% raw %}
{% include twittercards.html %}
{% endraw %}
{% endhighlight %}

### 3) Validate your links for Twitter Cards

Now, once you have added the code in your `head.html`, you need to update the source trunk of your Jekyll blog and validate your links from [here](https://cards-dev.twitter.com/validator). This will also add your site in the whitelist for the future validation.

![]({{baseurl}}/media/images/twitter-summary-card-preview.png)

## Conclusion

In this blog post, I have provided the information on Adding the Twitter Cards to Jekyll and how it can be used to optimise the sharing of your blog posts. If you have any questions, then ask in the comments section below. Why not follow me on [Twitter](http://twitter.com/danyalzk) and [Facebook](http://facebook.com/danyal.zia.k)?
