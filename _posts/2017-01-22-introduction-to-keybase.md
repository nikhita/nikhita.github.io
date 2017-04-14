---
layout: post
title: Introduction to Keybase
description: An introduction to keybase and why you should use it.
comments: true
---

Ever since I heard of [Keybase](https://keybase.io/), I wanted to join it. Unfortunately, when I first set my sight on it, it required an invitation to sign up. (At the time of writing this, Keybase does not require an invite even though the landing page of the website says otherwise. In case you need an invite, hit me up!)

The concept of Keybase seems to be easy to understand…once you have understood it! When I first heard of it, I was confused. It took me some googling to figure out what it really was. Hope this post clears all the fuzzy theories you have about Keybase. :)


### What is Keybase

Keybase is a trusted storehouse of public keys. If I want to send you an encrypted message, I can easily find your public key. However, I want to be sure that it is indeed _you_ to whom I am sending the message - this is where the trust factor creeps in.

Keybase establishes trust by connecting to your social accounts. It will require you to post on each of your accounts - claiming them and linking back to your keybase account. So now I get to verify your identity and know that the person claiming to be you on twitter is actually you (as with github, etc). This reinforces my conviction in your public key and makes me feel comfortable in sending you the message.

Keybase has four main 'features':

* **Establishes identity**: Keybase solves the problem of fake accounts by making you ‘prove’ your online identity - twitter, github, etc. Essentially, you are claiming your accounts and hence your identity. Once you do this, people can feel comfortable sending you messages even if they haven’t met you IRL. This is also known as the Web of Trust. 
You will have to post something on twitter, github gists, etc to tell everyone that you control these accounts. 

* **Storehouse of public keys**: Keybase can be considered as a storehouse with easily searchable public keys. This is quite handy if you want to send/recieve encrypted messages - it eliminates the need to share the key with the person separately.

* **Protection against hacks**: Keybase associates each device you own with an encryption key. If one of your devices get hacked, you can remove that device from your Keybase identity. So people now know that one of your devices was hacked and they won’t send messages to that device anymore.

* **The awesome file system**: Keybase also has a file system of its own called KBFS. In simple terms, it’s a secure way of file sharing. There are two types of folders - public and private. Everything in your public folder is signed by you and private folders are end-to-end encrypted which means even Keybase can’t see them!

### Setting up your account

Note: The following is primarily meant for Linux.

Head to the [website](https://keybase.io/) and join. After joining, [install](https://keybase.io/download) the keybase app for your desktop. Start keybase by:

{% highlight bash %}
$ run_keybase
{% endhighlight %}

This is will open a GUI where you can login. If you prefer to use the CLI:

{% highlight bash %}
$ keybase login
$ keybase pgp select    # if you already have keys
{% endhighlight %}

Be cautious about adding your private key to the Keybase server. It _might_ be safe but your private key is meant for your eyes only - better to keep it that way.

You can add devices to your keybase account. Each device comes with an encryption key. In case any of your devices is compromised, remove it from your account. Keybase also "tracks" users you follow. So if any user has their device compromised, it will let you know.

The mobile apps are still in development. Until then, you can use something called as "paper keys". They are NaCl keys which can be used to provision a new computer. It's a series of words out of which the first two words are the public label and the rest encodes the private key.

{% highlight bash %}
$ keybase device add
$ keybase paperkey
{% endhighlight %}

### Establishing your identity

It will prompt you to post tweets, gists or what have you to tell everyone: "The person who owns all these accounts is the same - ME! ME! ME!" (obviously not literally).


{% highlight bash %}
$ keybase prove twitter
$ keybase prove github
{% endhighlight %}

<br>
<div align="center">
<blockquote class="twitter-tweet" data-lang="en"><p lang="ht" dir="ltr">Verifying myself: I am nikhita on Keybase.io. cpc3RA8ONsz-83w_F1AngE311_N2CXo2AODV / <a href="https://t.co/VJlCsJp3i2">https://t.co/VJlCsJp3i2</a></p>&mdash; Nikhita Raghunath (@TheNikhita) <a href="https://twitter.com/TheNikhita/status/820346838989598720">January 14, 2017</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>
</div>
<br>

Keybase creates a nice Merkel tree for you showing how your accounts and devices are connected. Note that you can use the paperkey to provision a second computer which would be shown as an arrow originating from the paperkey itself.

&nbsp;
<img alt="merkel-tree" src="{{ site.baseurl }}/assets/merkel-tree.png">
&nbsp;
<br>

### Sending encrypted messages

If you have added your private key on their server, you can use the website to encrypt and decrypt messages. In case you decide to do so, remember that encryption/decryption will happen in JS in your browser. So think twice!

If you haven't added your private key, then you'll have to use the CLI to encrypt or decrypt messages. 

{% highlight bash %}
$ keybase pgp encrypt nikhita -m "This is a test message!"
-----BEGIN PGP MESSAGE-----
Comment: https://keybase.io/download
Version: Keybase Go 1.0.18 (linux)

wcBMAzntlzkGOvi9AQgAZH3Fyv6U8C/OVbU8tgWqMec6qSWdQQsPH7rVm7y4KyN/
nDrZe3RhuS0i9HtfgnNbQipmzG2LcL6DN+KLhHvrYAhCa9TOg4sY8LVDe1aNw8Vg
T66AQ7LHsnTbK5z8HrngTIH3HnWEvuInUp+Tlqa47l2k3MX4FNdnf2TKJ7L/nVtN
x2vpkiGSE5iKj6AFsI11cv1WTuD48PNckBQpww5LJ8B4j8CCN5qw+gQfI85aMBYB
54JWLB64eWpjMYP/aoopkBopW6ZigViH6km7eAqG1Wf4BttHROWjmJqF0BvK9wYE
SN4I8Rt3f8PpDqh3OWrtXlZ5vmRUl1ckjFLStOGj1tLgAeRLWn4BcigIdZgCOnDk
fNyf4UeJ4AXg5uHe1uDd4sJahQfgNeRrgQbnI5T54dwSwuFD3ZHR4H/iko70juAW
4aey4C7kcbElZkcUaEDGFGZX0fXNF+IFrDLI4Zo1AA==
=CzPf
-----END PGP MESSAGE-----
{% endhighlight %}

That's it! Keybase will automatically search for my public key and use it to encrypt the message. Now you can send this encrypted block of text to me via any means - email, twitter, IM...anything! :)

I find this particularly handy because I don't have to go around asking for the public key. In fact, I don't even have to know the keybase username. I can send a message using the twitter account too.

{% highlight bash %}
$ keybase pgp encrypt TheNikhita@twitter -m "Hi again!"
{% endhighlight %}


To decrypt:

{% highlight bash %}
$ keybase pgp decrypt -m "encrypted-message-here"
{% endhighlight %}

More elaborate commands are available in the [documentation](https://keybase.io/docs/command_line).

### Using the file system

Keybase offers a secure and distributed file storage system (something like Dropbox). Unlike Dropbox, there is no sync model here - files are available on demand. This means that it does not take up any memory on your system. Also, each user in the alpha product is offered 10 GB of space.

* You can find this file system mounted at `/keybase/public/<username>` and `/keybase/private/<username>`. Instead of using my keybase username, my twitter (or other) username can also be used. `/keybase/public/TheNikhita@twitter` will also work.
* Everything that you store in the public folders is signed by you and everything that you store in private folders are end-to-end encrypted.
* Note that whatever you store in your public folder is visible at [https://keybase.pub/](https://keybase.pub/). To see a particular users file, go to `https://keybase.pub/<username>`.
* Private folders are named as `/keybase/public/nikhita,chris` or `/keybase/public/TheNikhita@twitter,chris`. This is an end-to-end encrypted folder where I can share secure files with Chris. You don't have to create such folders, they exist implicitly.

{% highlight bash %}
# to access public folders
cd /keybase/public/nikhita
cd /keybase/public/TheNikhita@twitter
cd /keybase/public/nikhita@github

# to access private folders between you and me
cd /keybase/private/nikhita,<your-username>
cd /keybase/private/TheNikhita@twitter,<your-username>
{% endhighlight %}

The best part of all this? If I am having a conversation with someone on twitter, I can simply say "That file is in our private folder on Keybase" without having to go through the hassle of asking for the public key!

### Conclusion

I love Keybase's goals and design. It is also [open source](https://github.com/keybase) -comforting! There might be security concerns if your account or device is compromised but these can be mitigated by revoking them. 

All in all, I like it and it would be exciting to see how it transitions from an alpha product in the future.



