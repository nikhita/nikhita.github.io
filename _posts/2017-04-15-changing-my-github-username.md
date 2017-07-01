---
layout: post
title: Changing my github username
description: So I did something crazy. Changed my github username. Now I have my first name as my github username.
comments: true
keywords: changing github username, change github username, reason to change github username, should I change github username
---

Yesterday someone asked my github username on Slack and I said `nikinath`. However, suddenly it just didn't feel right. My IRC and Slack username is `nikhita`. My Twitter handle is `TheNikhita` (want to change it too, awaiting response from the original account holder)...so it makes sense to keep my Github username as just `nikhita`, right?

It's more professional and easier to link people to my work. Also, it makes things simpler while discussing on IRC and Slack - avoids all the overhead of asking for the GitHub username. It's even easier for people to remember you! ;)

But honestly, the real reason? It's just really COOL!
<br>
<br>

### Github username squatting

A quick google search told me that the username was already taken by someone. However, the user holding the account had absolutely zero activity since...forever (okay, 2011). But zero repos, zero stars, zero followers, zero...you get the gist (even zero gists, hehe).

Then I came across Github's [username squatting policy](https://help.github.com/articles/name-squatting-policy/) and immediately clicked the _Contact a human_ button on the page and sent them this request:

<br>
<blockquote>
Hi,<br><br>

I'd like to know if the username `nikhita` can be released? The user who has registered that username doesn't seem to have any activity at all (from 2011).<br><br>

My first name is Nikhita so I'd like to have `nikhita` as my username. Currently, I own `nikinath`.<br><br>

Please let me know if this is possible. Would be really awesome if it can be done!<br><br>

Cheers,<br>
Nikhita
</blockquote>
<br>
Within **15 minutes**, I get the following response:

<br>
<blockquote>

Hi Nikhita,<br><br>

You are in luck — we have classified the ** nikhita** account as inactive and released the username for you to claim, as per our Name Squatting Policy:<br><br>

https://help.github.com/articles/name-squatting-policy<br><br>

Be quick, as the username is now publicly available. Glad to help!<br><br>

Thanks,<br><br>

Jacqui

</blockquote>
<br>
Github's customer service has always been phenomenal. Never failed me.

Happily, I changed my username and waited for things to break.
<br>
<br>

### Everything breaks!

Thankfully, I decided to change the username sooner than later. There aren't _that_ many things linked to my username currently.

I put on my imaginary save-your-github-account-from-doom gloves and did the following:

* updated all my remotes: `git remote set-url origin git://new.url.here`. Revisited a lot of my repos/forks and updated them.

* Let some people know about the username change so they can update on their side.

* Made a dummy github account with the old username [`nikinath`](https://github.com/nikinath) to help with redirects.

* I share a lot of gists with people on slack/irc. Thankfully, slack provides allows you to edit the messages. So, I edited the gist links in case someone clicks on it in the future (unlikely, but still).

* Some of my work involves having signed the [CNCF CLA](https://github.com/cncf/cla). So updated in the Linux Foundation ID.

* Changed the link on Keybase, Twitter, etc.

* My website is hosted on Github pages which generates the domain name from the username. I did a `grep -rn "nikinath"` in my website repo. YIKES.

    - made the relevant changes from `nikinath` to `nikhita`
    - updated Google Analytics
    - updated Disqus
    - resubmitted to Google Webmaster Tools
    - created a new remote repo `nikhita.github.io` and made my local repo track this.
    - pushed changes and make sure it works. If you are reading this, then yes, it worked. :D

* Hope nothing else has broken.

### Gotchas

There a few things you should know about changing the username:

* One place where the change doesn't occur is in PR comments. If someone commented with an @-mention to you using **@old-username**, it won't redirect/change to **@new-username**. So I would advice you to create a new account with your old username to help with such redirects.

* If you had initially set your email id as private, the commits you made directly using the Github UI will now be referenced to the old username. If you don't create a new account to squat on the old one, these commits will be shown as committed by a "Ghost" user and will not be attributed to you. However, any commits you made using Git will be appropriately attributed to your new username.

* Basically, you need to change all places where your old username occurs like _README_, etc. Pro-tip: A Github search of your old username will turn out to be very useful in this case.

* It will probably take a week or two for search engines to index your new account. So if someone googles you, they will be taken to a broken link to your old one. Another reason why you should probably consider squatting on the old username. :wink:

* Someone asked me on Twitter if the change is also reflected in Gitter. Well, guess what? It is!

### Let the world know
<div align="center">
<blockquote class="twitter-tweet" data-conversation="none" data-lang="en"><p lang="en" dir="ltr">.<a href="https://twitter.com/github">@github</a> Wohoo now I have my first name as my <a href="https://twitter.com/github">@github</a> username! 😎</p>&mdash; Nikhita Raghunath (@TheNikhita) <a href="https://twitter.com/TheNikhita/status/852901534912307200">April 14, 2017</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>
</div>
<br>

If you are ever planning to go down the username change road, may the Force be with you.

PS: Needless to say, my github profile is now at: [https://github.com/nikhita](https://github.com/nikhita).





