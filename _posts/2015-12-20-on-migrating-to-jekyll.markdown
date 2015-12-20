---
layout: post
title:  "On Migrating To Jekyll"
date:   2015-12-20 9:53 PM
tags:
---

I’ve just finished migrating this blog to [Jekyll](http://www.jekyllrb.com), and in short, I’m pretty happy with the results. It has only taken me a few days to set up, migrate all previous posts, find and modify a slick theme and migrate the domains to GitHub Pages[^1]. That’s not to say the road was easy. Heck, it was interesting enough that I felt the need to write a blog post about it.

{% include lightbox.html image="React_Blog_UI.png" caption="The dreaded 'before' image" %}

## Motivation Behind The Old Blog
TI set out on building the previous version of this blog as a means of learning [React.js](http://https://facebook.github.io/react/). I often look at frameworks, languages and platforms that I find interesting and feel unfulfilled by simply following the main tutorial on their website.

The tutorials that I would consider "good" often only result in the developer setting up some sort of contrived application such as a basic hello world, echo server or todo list app, which to me seems like a great introduction, but is not enough to build a solid opinion on. At the time that I set up the blog I had a burgeoning interest in React and had wanted to experiment with doing a more graphically oriented form of development, as the majority of my serious experience thus far has primarily involved server-side programming and CLI applications.

## The 1 Year Itch
I had originally aimed to build the blog in a piecemeal fashion in order to satisfy my needs. Unfortunately, I’m not great with web design work, and it didn't take the full 12 months for me to realise this. Working on the blog there eventually came a point where I felt that I’d need to implement a number of features that would take quite a while to develop.

The requirement of things like a blog index, pagination and better aesthetics introduced quite a large barrier for me to actually want to bother to write anything, since I felt that they were already pressing issues that would only become more urgent as I added more content. Coupled with the long load times, and the cost of running a very basic static site on an otherwise unused EC2 instance and I saw no reason to continue experimenting with React in this way. I needed to change.

## Along Comes Jekyll
The blog is now a static Jekyll site, using a modified version of the [Centrarium](http://www.bencentra.com/centrarium) theme. The migration to jekyll wasn’t completely smooth sailing as I did face a number of challenges, though most of them revolved around the customisations I wished to make to the theme for my use case and my inexperience with Jekyll.

### Custom Includes
One of the post elements that I made use of since my very first blog post was a quote element. The thinking behind this feature was that as I wrote an article on a topic I could include some easily identifiable quotes about the subject matter. As well as this I wanted to be able to include images in my posts that would always make use of the Lightbox script when they were clicked on. To accomplish this I made use of Jekyll includes, which allow me to add commonly used components to my posts that follow a common structure without a heap of code duplication.

~~~~~{% raw %}
{% include lightbox.html image="React_Blog_UI.png" caption="Former blog" %}
{% endraw %}~~~~~

~~~~~{% raw %}
<a href="{{site.images}}/{{include.image}}" data-lightbox="{{include.image}}" data-title="{{include.caption}}">
   ![{{include.caption}}]({{site.images}}/{{include.image}})
</a>
{% if include.caption %} <span>{{ include.caption }}</span> {% endif %}
{% endraw %}~~~~~

### Better Disqus Functionality
The existing Disqus integration in the theme made it simple for me to get Disqus comments up and running. This was a real boon for me, as Disqus integration was something that I had always wanted to do for my previous blog and was dreading having to figure out. There were some minor issues I encountered however. While I was testing the site locally a large number of discussions were created on Disqus for links from localhost:4000.

Thankfully, Disqus makes it pretty easy to resolve this problem, all it required was the setting up of some configuration variables in the code and use of the [URL Mapping tool](https://help.disqus.com/customer/portal/articles/912757-url-mapper) to merge the erroneously created conversations. In addition to this I added comment counts to the blog index.

~~~~~{% raw %}
var disqus_config = function () {
 this.page.url = "{{site.disqus_baseurl}}{{page.id}}";
 this.page.identifier = "{{page.id | replace: '/', ''}}";
 this.page.title = "{{page.title}}";
};
{% endraw %}~~~~~

### Previous and Next post links
This was the most significant user-facing modification I made to the theme, and was quite simple to implement. I made use of some of the CSS and Liquid Templating Language from a [post by David Elbe](http://david.elbe.me/jekyll/2015/06/20/how-to-link-to-next-and-previous-post-with-jekyll.html) and applied some styling that better suited the site and was already in use elsewhere. You can see these in effect at the bottom of this post.

### Migrating the Domains
This was a particularly painful ordeal for me as I was keen to finish this "little" weekend project. It was the last thing necessary in order to get the blog live on the air and, as it turns out, is an outright unsupported use case for GitHub Pages.

I had two domains pointing at the old blog[^1], and the new blog needed to be accessible from both those domains as well. In order to route traffic to your site when using a custom domain GitHub Pages sends the traffic to the repository with your custom domain in the CNAME file in the root of the repository. One limitation of this system is that each repository can only be accessed from one custom domain.

The workaround for this that I settled on was to create a GitHub organisation and build a project page. The only difference between the two repositories are that each CNAME file contains a different one of my domains. In order to keep the two repositories up to date I’ve added the organisation repository as another remote for the personal GitHub Pages repository. I’m yet to look into an automated solution for keeping these two repositories in sync.

## Conclusion and Outlook
There are still a number of changes and tweaks I'd like to make to the blog, and these are very quickly filling up the Backlog list on my Trello board for this site. All in all though, I’m quite happy with how the blog has turned out.

I’ve got a much nicer looking blog, packed with a handful of extra features to both provide a better experience for readers and to make my life easier, hopefully taking away one of my excuses for not writing more often.

[^1]: [MichaelHudson.net.au](http://MichaelHudson.net.au) and [IAmMichaelHudson.com](http://IAmMichaelHudson.com)
