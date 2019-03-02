---
layout: post
title: How to build a blog using Github, Jekyll and Lanyon
description: This is a detailed tutorial for making your blog using Github pages. It covers every thing that you need to do - step by step!
comments: true
---
UPDATE: I redesigned this blog using [Centrarium](https://github.com/bencentra/centrarium). Though my blog does not reflect the steps in this post, this tutorial helped me to rebuild my blog. I hope this helps you too!

I built this blog using Github pages, [Jekyll](http://jekyllrb.com) and the [Lanyon](http://lanyon.getpoole.com/) theme. The most amazing part is that it's free, minimalist, uses Markdown and you can get it running in no time! Also, it does not feel bloated like Wordpress, etc.

Here's a short tutorial on how I made this blog. Ready to learn? Let's get started!

**Note: If you are not interested to do the setup yourself, simply fork [my repo](https://github.com/nikhita/nikhita.github.io) and make the changes to include your details.**

## Table of Contents:

1. [Installing Jekyll](#installing-jekyll)
2. [Using Lanyon](#using-lanyon)
3. [Exploring the directory structure](#dir-struct)
4. [Modifying configuration file](#config)
5. [Adding an archive page](#archive)
6. [Integrating Disqus comments](#disqus)
7. [Enabling Google Analytics](#ga)
8. [Adding custom favicon](#favicon)
9. [Adding your photo to the sidebar](#photo)
10. [Adding social media buttons](#social-media)
11. [Changing the font](#font)
12. [Other tips](#other-tips)
13. [Conclusion](#conclusion)


## <a name="installing-jekyll"></a>1. Installing Jekyll

We are going to use Jekyll as a static site generator to build our website. Jekyll is written in Ruby and requires Ruby to be installed on your system. Chances are, you already have ruby installed. But Jekyll 2 requires v1.9.3 or greater and Jekyll 3 requires v2.0 or greater. Here, we'll use v2.0. Note that we'll also need the development headers. So go ahead and type this in your terminal:

```shell
$ sudo apt-get install ruby2.0 ruby2.0-dev
```

Now, check your ruby version using:

```shell
$ ruby --version
```

When I type that into my terminal, I get something like this: ```ruby 2.0.0p384 (2014-01-12) [x86_64-linux-gnu]```. If you find some other ruby version as your default version, you'll need to set this as your default one. For this, you can use RVM.

```shell
$ sudo apt-get install zlib1g-dev build-essential libssl-dev libreadline-dev libyaml-dev libsqlite3-dev sqlite3 libxml2 libxml2-dev libxslt-dev gawk libgdbm-dev libncurses5-dev automake libtool bison libffi-dev nodejs
\curl -sSL https://get.rvm.io | bash -s stable
```

Then set the default ruby version using (you can use other ruby versions as well):

```shell
$ rvm --default use 2.0.0
```

You'll also need Rubygems - which is a package management framework for Ruby. You can download it from  [here](https://rubygems.org/pages/download/). Now, we can finally install jekyll!

```shell
$ gem install jekyll
```

Great, now we can proceed to use Lanyon! :)

## 2. <a name="using-lanyon"></a>Using Lanyon

I like the Lanyon theme since it focuses more on content and is minimalistic. If you are not a fan of sidebars, you can checkout [Poole](http://demo.getpoole.com/) or if you prefer a static sidebar, have a look at [Hyde](http://hyde.getpoole.com/). Decided on your theme? Let's move ahead!

First of all, you will need to create a repository having the name _username.github.io_. For example, my Github username is _nikhita_ so I have named by repo as _nikhita.github.io_. After you do this, clone this repository onto your local computer. Replace ```username``` with your real username.

```shell
$ git clone https://github.com/username/username.github.io.git
```

Next, download the Lanyon zip file from [here](https://github.com/poole/lanyon/archive/master.zip) and extract it into your _username.github.io_ folder. Alternatively, you can fork the Lanyon repo and change the forked repository's name as _username.github.io_. After that, clone the forked repo onto your local computer.

Now, let's move into our folder and run the default page on our local server.

```shell
$ cd username.github.io
$ jekyll build
$ jekyll serve
```

Open up your browser and go to: http://localhost:4000 and voila, the website is hosted locally on your system and is ready to be tweaked! 

## <a name="dir-struct"></a>3. Exploring the directory structure

Before we go ahead and make customizations, let's have a look at the files in your folder. Once we learn the design, we can go ahead and make changes confidently! 

```shell
.
|-- 404.html
|-- about.md
|-- atom.xml
|-- _config.yml
|-- _includes
|   |-- head.html
|   `-- sidebar.html
|-- index.html
|-- _layouts
|   |-- default.ht_ml
|   |-- page.html
|   `-- post.html
|-- LICENSE.md
|-- _posts
|   |-- 2013-12-31-whats-jekyll.md
|   |-- 2014-01-01-example-content.md
|   `-- 2014-01-02-introducing-lanyon.md
|-- public
|   |-- apple-touch-icon-precomposed.png
|   |-- css
|   |   |-- lanyon.css
|   |   |-- poole.css
|   |   `-- syntax.css
|   `-- favicon.ico
`-- README.md
```

Here is a brief explanation of what you see: 

* When you run Jekyll, it creates a folder called _site with the static website inside it. Every file or folder in the repo will get copied into the _site folder unless it begins with an underscore.
* _config.yml is the configuration file, which is the first file we are going to change.
* index.html is your front page and about.md is a static page. You can add other static pages by creating markdown files (which we will be doing further). 404.html is pretty self-explanatory.
* atom.xml is for the RSS reader.
* _includes and _layouts folders contain the boilerplate HTML required to build the site. 
* _posts include the posts that you'll be...well...posting. They are Markdown files. 
* public contains [favicon](https://en.wikipedia.org/wiki/Favicon) information and CSS files. 

Still with me? Let's do some tweaking! :)

## <a name="config"></a>4. Modifying configuration file

The first thing you want to do is change the ```_config.yml``` file. Open it in your favorite text editor and edit the sections in _Setup_  and _About/contact_ according to your preferences. 

You can add other details as well. Have a look at [my _config.yml](https://github.com/nikhita/nikhita.github.io/blob/master/_config.yml) for reference. 

Lanyon is built on Poole and Poole does not support Jekyll 3 yet. You can check [this issue](https://github.com/poole/lanyon/issues/124). For this, you'll need to add:

{% highlight yaml %}
gems: [jekyll-paginate]
paginate_path: "page:num" 
{% endhighlight %}

and comment out: ```relative_permalinks: true```.

Now we are good to go!


## <a name="archive"></a>5. Adding an archive page

Lanyon, by default, does not provide an archive page. So let's make one. In your root folder, create an ```archive.md``` file and add the following contents to it. 

```ruby
{% raw %}
---
layout: page
title: Archive
---


{% for post in site.posts %}
  * {{ post.date | date_to_string }} &raquo; [ {{ post.title }} ]({{ post.url }})
{% endfor %}
{% endraw %}
```

Now run the following commands again and go to http://localhost:4000 to see the Archive page on your website. Note that we'll be making lots of changes so it's a good idea to keep checking what changes you are making. So keep these commands in mind!

```shell
$ jekyll build
$ jekyll serve
```

## <a name="disqus"></a>6. Integrating Disqus comments

Obviously you'll need a Disqus account for this. Head to the website, create an account and it'll ask you if you want to "Add Disqus to your site". If you already have an account, click on the gear icon on the top right corner and select the option. Follow the steps until it gives you a _shortname_ for your website. 

Now open the ```_layouts/default.html``` file and add the line as shown:

```html
<div class="container content">
  {% raw %}
  {{ content }}
  {% include comments.html %}
  {% endraw %}
</div>
```


The parent ```div```s are wider than the content container so adding the include statement outside of this one will make the comments section stretch across the entire page, rather than being confined to the content’s area.

Now that you have included ```comments.html```, let's create it! Create a file called ```comments.html``` in the ```_includes``` folder and add the following lines. Make sure that you replace _your-shortname-here_ with your actual shortname.

```html
{% raw %}
{% if page.comments %}
<div id="disqus_thread"></div>
<script type="text/javascript">
    /* * * CONFIGURATION VARIABLES * * */
    var disqus_shortname = 'your-shortname-here';
    /* change the above line to include your real shortname */
    var disqus_identifier = "{{ site.disqusid }}{{ page.url | replace:'index.html','' }}";
    
    /* * * DON'T EDIT BELOW THIS LINE * * */
    (function() {
        var dsq = document.createElement('script'); dsq.type = 'text/javascript'; dsq.async = true;
        dsq.src = '//' + disqus_shortname + '.disqus.com/embed.js';
        (document.getElementsByTagName('head')[0] || document.getElementsByTagName('body')[0]).appendChild(dsq);
    })();
</script>
<noscript>Please enable JavaScript to view the <a href="https://disqus.com/?ref_noscript" rel="nofollow">comments powered by Disqus.</a></noscript>
{% endif %}
{% endraw %}
```

Note that the comments will not run if you don't set ```comments``` to ```true``` in the YAML frontmatter of the posts. So open any post (say, _2014-01-02-introducing-lanyon.md_) from the _posts folder and add the following line on top:

{% highlight yaml %}
---
layout: post
title: Introducing Lanyon
comments: true /*add this line*/
---
{% endhighlight %}

Now run ```jekyll build``` and ```jekyll serve``` again to see Disqus comments enabled on the post! :)

## <a name="ga"></a>7. Enabling Google Analytics

Again, you'll need a GA account for this. In the Admin tab, you'll find _Tracking info_ under the _Property_ section. Under that you'll find a _tracking code_ with a script. Something like this:

```html
{% raw %}
<script>
  (function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
  (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
  m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
  })(window,document,'script','https://www.google-analytics.com/analytics.js','ga');

  ga('create', 'UA-82647777-1', 'auto');
  ga('send', 'pageview');

</script>
{% endraw %}
```

Create a file called ```google_analytics.html``` in the ```_includes``` folder and add the the code GA gave you. Do not paste the code I posted above - you'll mess up my stats! :(

Now add the following line in ```default.html``` inside the ```_layouts``` folder. 

```html
{% raw %}
  <body>
    {% include google_analytics.html %} /*add this line*/
    {% include sidebar.html %}
{% endraw %}
```

Save it and you are good to go!

## <a name="favicon"></a>8. Adding a custom favicon

You can create a [favicon](https://en.wikipedia.org/wiki/Favicon) using GIMP or you can use an easy online [option](http://faviconit.com/en). I rolled the online way. 

If you plan to use the online method, extract the files to the ```public``` folder (which should have a placeholder ```favicon.ico```). 

Go to ```head.html``` in _includes and add the following line:

```html
<!-- Icons -->
<link rel="icon" sizes="16x16 32x32 64x64" href="{{ site.baseurl }}/public/favicon.ico">
```

Note: If you used the link that I provided, you'll have many other images. Have a look at the readme file provided after extraction and change the href link to include ```{% raw %} {{ site.baseurl }}/public/ {% endraw %}```. Look at my [head.html](https://github.com/nikhita/nikhita.github.io/blob/master/_includes/head.html) to understand it better. 

Cool, now we have got our custom favicon in action!

## <a name="photo"></a>9. Adding your photo to the sidebar

We'll use [Gravatar](http://en.gravatar.com/) for this. Go to the website, create an account and upload your image. According to the instructions [here](http://en.gravatar.com/site/implement/hash/), you'll need the md5 hash. For this, you'll need to type a php command. Go [here](http://phpfiddle.org/) and run:

```php
echo md5(strtolower(trim("MyEmailAddress@example.com")));
```

You'll get a md5 hash. Copy the hash and add it in your _config.yml file as shown:

```yaml
#About/contact

gravatar_md5: your-md5-hash-here
```

Then open your sidebar.html file and add this line:

```html
<div class="sidebar" id="sidebar">

/*add the following lines*/
 <div class="sidebar-logo" style="align:center">
      <img src="http://www.gravatar.com/avatar/{{ site.author.gravatar_md5 }}?s=120" />
  </div>
```

To make your photo look good on the sidebar, create a ```custom.css``` file in ```public/css``` and add the following lines:

```css
.sidebar-logo {
      padding: 1.5rem;
}
  
.sidebar-logo img {
      border-radius: 50%;
      -moz-border-radius: 50%;
      -webkit-border-radius: 50%;
      width: 160px;
      margin: 0 auto;
}
```

Save it, run your server and look at your pretty picture on the sidebar! :)

## <a name="social-media"></a>10. Adding social media buttons

I have used icons from the [Font Awesome](http://fontawesome.io/) library. If you don't like the icons I used, you can choose other icons of your own - after all, it's your website!

Add the following line with other CSS links in ```_includes/head.html```:

```html
<link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/font-awesome/4.3.0/css/font-awesome.min.css">
```

In your ```sidebar.html``` setup a div container for all these icons to go in:

```html
<div id="contact-list" style="text-align:center">
<!-- contact icons go here --> 
</div>
```

You can link multiple social media accounts in the div. For example, if you want to link your LinkedIn account, add the following lines:

```html
{% if site.author.linkedin %}
        <a href="https://linkedin.com/in/{{ site.author.github }}">
          <span class="fa-stack fa-lg">
            <i class="fa fa-square-o fa-stack-2x"></i>
            <i class="fa fa-linkedin fa-stack-1x"></i>
          </span>
        </a>
      {% endif %}
```

For email, ```href="mailto: {{ site.author.email }}"``` and for rss, ```{% raw %} href="{{ site.url }}/atom.xml" {% endraw %}```.

Awesome, our social media buttons are ready for action!

## <a name="font"></a>11. Changing the font

Personally, I didn't like the default Lanyon font. Head over to [Google Fonts](https://fonts.google.com/?authuser=1) and choose a font that you love. Google will provide you with a stylesheet link. Something like this:

```html
<link href="https://fonts.googleapis.com/css?family=Average" rel="stylesheet"> 
```

Add this line to ```head.html``` in the list of CSS links. Now, go to ```public/css/lanyon.css``` and your font to the ```font-family```.

```css
/* I added the Average font here */
html {
  font-family: "Average", "PT Serif", Georgia, "Times New Roman", serif;
}
```

Finally, you have even changed your fonts! Yay!

## <a name="other-tips"></a>12. Other tips

Some hacks to make your blogging experience better:

* Set up a ```_drafts``` folder in your root directory. Save the posts without the date, eg: ```title-without-date.md```. In order to preview this, run

```shell
$ jekyll serve --drafts
```

* For adding images to your site, you can setup an ```images``` folder and use the images with ```{% raw %} <img src="{{ site.baseurl }}/images/file-name-here"> {% endraw %}```.

## <a name="conclusion"></a>13. Conclusion

### References

* [Joshua Lande's post](http://joshualande.com/jekyll-github-pages-poole)
* [Kyle Stratis's post](http://kylestratis.com/2015/04/17/blog-setup/)
* [Patrick Steadman's post](http://patricksteadman.ca/2014/08/04/lanyonsetup/)

Hope this blog post helps you! :)
