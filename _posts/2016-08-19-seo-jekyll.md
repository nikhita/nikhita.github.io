---
layout: post
title: SEO for Jekyll blogs
description: This is a detailed tutorial for making your SEO compatible. It covers every thing that you need to do - step by step!
comments: true
image: /images/seo-example.jpg
---

Previously, I wrote about [how to make a Jekyll blog](https://nikhita.github.io/build-blog-using-github-jekyll). In this post, I'll talk about how you can make that blog SEO compatible. 

Jekyll blogs don't have any SEO functionality by default so I had to incorporate it myself. This led me to learn more about SEO and it turned out to be quite a fun experience!

Here is a detailed tutorial on what you need to do to make your Jekyll blog SEO compatible. Note that it's **highly recommended** that you do this since your Jekyll blog isn't indexed - and Google needs your site to be indexed to be included in the search results.

## Table of Contents:

1. [Title, description and keywords](#title-description)
2. [The jekyll-seo-tag plugin](#plugin)
3. [Adding sitemap.xml](#sitemap)
4. [Adding robots.txt](#robots)
5. [Adding share buttons for social media](#share)

## <a name="title-description"></a>1. Title and description

The most important part of SEO is that you need to have a title and description. Keywords are usually not necessary. You can mention these in the YAML frontmatter of the posts as shown:

```yaml
---
layout: post
title: your-title-here
description: your-description-here
keywords: keyword1, keyword2, keyword3
---
```

Mentioning the title, description and keywords help you to be ranked higher. Also, if your first paragraph and the context of the whole post differ, this would turn out to immensely useful.

Now that you have mentioned it in your post, you'll need to include these meta. This can be done by adding the following lines in ```head.html```. Note that the title meta is already included by default. 

```html
 <!-- add description and keywords for SEO -->
 {% raw %}
  <meta name="description" content="{% if page.description %}{{ page.description }}{% else %}{{ site.description }}{% endif %}">
  {% if page.keywords %}
 <meta name="keywords" content="{{ page.keywords }}" />
  {% else %}
 <meta name="keywords" content="your-default-comma-separated-keywords" />
 {% endif %}
 {% endraw %}
```

## <a name="plugin"></a>2. The jekyll-seo-tag plugin

Github [officially endorses](https://help.github.com/articles/search-engine-optimization-for-github-pages/) the jekyll-seo-tag plugin to enable SEO on github pages. Ofcourse, you can use it on your site as well. And it's really, really simple to do so. Include the following gem in your ```_config.yml``` file:

```yaml
gems:
    -jekyll-seo-tag
```

Add this one line in your head tag or the ```head.html``` file:

```html
{% raw %}
{% seo %}
{% endraw %}
```

Wasn't that easy? Told ya!

## <a name="sitemap"></a>3. Adding sitemap.xml

The sitemap is a xml file to help bots crawl your website easily. Also, it's a good idea to submit sitemaps to search engines so that they don't have to look for it in the first place. 

You can use a [plugin](https://github.com/jekyll/jekyll-sitemap) for making it but I wanted my site to be more GWT-friendly (Google Webmaster Tools). GWT doesn't like relative URLs and the plugin doesn't put absolute URLs in the sitemap. But fret not! You can make it yourself too. Simply make a file called ```sitemap.xml``` in your root directory and paste the following code:

```xml
{% raw %}
---
layout: null
sitemap:
  exclude: 'yes'
---
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  {% for post in site.posts %}
    {% unless post.published == false %}
    <url>
      <loc>{{ site.url }}{{ post.url }}</loc>
      {% if post.sitemap.lastmod %}
        <lastmod>{{ post.sitemap.lastmod | date: "%Y-%m-%d" }}</lastmod>
      {% elsif post.date %}
        <lastmod>{{ post.date | date_to_xmlschema }}</lastmod>
      {% else %}
        <lastmod>{{ site.time | date_to_xmlschema }}</lastmod>
      {% endif %}
      {% if post.sitemap.changefreq %}
        <changefreq>{{ post.sitemap.changefreq }}</changefreq>
      {% else %}
        <changefreq>monthly</changefreq>
      {% endif %}
      {% if post.sitemap.priority %}
        <priority>{{ post.sitemap.priority }}</priority>
      {% else %}
        <priority>0.5</priority>
      {% endif %}
    </url>
    {% endunless %}
  {% endfor %}
  {% for page in site.pages %}
    {% unless page.sitemap.exclude == "yes" %}
      {% unless page.url contains 'index.html' %}
      <url>
        <loc>{{ site.url }}{{ page.url | remove: "index.html" }}</loc>
        {% if page.sitemap.lastmod %}
          <lastmod>{{ page.sitemap.lastmod | date: "%Y-%m-%d" }}</lastmod>
        {% elsif page.date %}
          <lastmod>{{ page.date | date_to_xmlschema }}</lastmod>
        {% else %}
          <lastmod>{{ site.time | date_to_xmlschema }}</lastmod>
        {% endif %}
        {% if page.sitemap.changefreq %}
          <changefreq>{{ page.sitemap.changefreq }}</changefreq>
        {% else %}
          <changefreq>monthly</changefreq>
        {% endif %}
        {% if page.sitemap.priority %}
          <priority>{{ page.sitemap.priority }}</priority>
        {% else %}
          <priority>0.3</priority>
        {% endif %}
      </url>
      {% endunless %}
    {% endunless %}
  {% endfor %}
</urlset>
{% endraw %}
```

After that go ahead and [submit](https://support.google.com/sites/answer/100283?hl=en) it to Google. 

Great, your website is almost SEO-ready! 

## <a name="robots"></a>4. Adding robots.txt

```robots.txt``` is a text file that instructs robots (typically search engine robots) on how to search and index pages. Create a ```robots.txt``` file in your root directory and paste the following code. Don't forget to properly mention your site url.

```
User-agent: *
Sitemap: your-site-url/sitemap.xml
```

That's it for ```robots.txt```!

## <a name="share"></a>5. Adding share buttons for social media

This isn't technically SEO but it helps to grow your audience. If you'd like to implement the share buttons like I did, make a html file called ```share.html``` in the ```_includes``` folder and paste the code below (Source: [webjeda](https://blog.webjeda.com/)):

```html
{% raw %}
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/font-awesome/4.5.0/css/font-awesome.min.css">

<h3 class="share-this">Share this!</h3>
<div id="share-box"> 
        <a href="https://www.facebook.com/sharer/sharer.php?u={{ site.url }}{{ page.url }}" onclick="window.open(this.href, 'mywin',
'left=20,top=20,width=500,height=500,toolbar=1,resizable=0'); return false;" ><i class="fa fa-facebook-official fa share-button"></i></a>
       
        <a href="https://twitter.com/intent/tweet?text={{ page.title }}&url={{ site.url }}{{ page.url }}" onclick="window.open(this.href, 'mywin',
'left=20,top=20,width=500,height=500,toolbar=1,resizable=0'); return false;"><i class="fa fa-twitter fa share-button"></i></a>
       
        <a href="https://plus.google.com/share?url={{ site.url }}{{ page.url }}" onclick="window.open(this.href, 'mywin',
'left=20,top=20,width=500,height=500,toolbar=1,resizable=0'); return false;" ><i class="fa fa-google-plus fa share-button"></i></a>
       
        <a href="http://www.reddit.com/submit?url={{ site.url }}{{ page.url }}" onclick="window.open(this.href, 'mywin',
'left=20,top=20,width=900,height=500,toolbar=1,resizable=0'); return false;" ><i class="fa fa-reddit fa share-button"></i></a>
       <a href="https://www.linkedin.com/shareArticle?mini=true&url={{ site.url }}{{ page.url }}&title={{ page.title }}&summary={{ page.description }}&source=webjeda" onclick="window.open(this.href, 'mywin',
'left=20,top=20,width=500,height=500,toolbar=1,resizable=0'); return false;" ><i class="fa share-linkedin fa-linkedin fa share-button"></i></a>                         
        <a href="mailto:?subject={{ page.title }}&amp;body=Check out this site {{ site.url }}{{ page.url }}"><i class="fa fa-envelope fa share-button"></i></a>                                  
</div>
{% endraw %}
```


Now you need to include this html file. I just wanted it to appear on my _posts_ page (and not on home page, 404 page, etc) so I included it in ```_layouts/post.html```. I included it just above the final ending div tag.

```html
{% raw %}
{% include  share.html %}
{% endraw %}
```

Let's make these buttons look pretty now! :)

Add these lines in a ```public/css/custom.css``` file:

```css
.share-button {
    margin: 0px;
    padding: 10px 20px 10px 20px;
    opacity: 0.9;
}

.share-button:hover {
    opacity: 1;
}

.share-this {
    text-align: center;
    padding-top: 50px;
}

#share-box {
    text-align: center;
    font-size: 40px;
    margin-bottom: 30px;
}

.fa-facebook-official {
    color: #3b5998;
    font-size: 40px;
}
.fa-google-plus {
    color: #d34836;
}

/* used share-linkedin here as fa-linkedin class is also used for sidebar. If fa-linkedin is used here, it colors even the sidebar */
.share-linkedin {
    color: #0077b5;
}
.fa-envelop {
    color: #444444;
}
.fa-reddit {
    color: #ff5700;
}

.fa-twitter {
    color: #4099FF;
}
```


Finally, we are done! Your website is now SEO-ready! :)

### Closing note

This article might not include _all_ the ways you can make your website come to the first page of Google but it's definitely a good start. Remember that the thumb rule is to write good content! :)

You can find the source code for this website [here](https://github.com/nikhita/nikhita.github.io).
