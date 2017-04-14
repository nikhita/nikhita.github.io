---
layout: post
title: Setting two factor authentication for Github
description: A simple guide to help you set up two factor authentication on Github and configuring git.
comments: true
---

When I heard of [2FA on Github](https://help.github.com/articles/about-two-factor-authentication/), I was excited and immediately enabled it. But enabling it brought it's fair share of problems and I was left scratching my head. I hope this post avoids that for you.

<br>

## Problems I faced

1. There was no SMS fallback option in India. I prefer the in-app authentication for generating the OTP but it would have been nice if I had the SMS option as well. This isn't a problem, I know, but it is annoying!
2. I could no longer push to Github. Now this was bad. Real bad.

```shell
$ git push origin master
Username for 'https://github.com': nikhita
Password for 'https://nikhita@github.com': 
remote: Invalid username or password.
fatal: Authentication failed for 'https://github.com/nikhita/nikhita.github.io.git/'
```
<br>

## How to solve it


**Generate a personal access token**: Github requires you to generate a Personal Access token for authenticating via the command line i.e. for git. To [generate](https://help.github.com/articles/creating-an-access-token-for-command-line-use/) this, go to Settings -> Personal Access Tokens -> Generate new token. Make sure you note down this token because you won't be able to see it again!

Test the token by:

```
$ curl -u <token>:x-oauth-basic https://api.github.com/user
```

You should see an output detailing your account. If something is wrong, you'll see a message like this:

```
{
  "message": "Not Found",
  "documentation_url": "http://developer.github.com/v3"
}
```


Now there are two ways to set up git for authenticating:

#### Using SSH

If you are using SSH, no additional steps are needed. Simply clone the repo, make the changes and then push. This way you won't have to specify the username or the password. There is a pretty handy [guide](https://help.github.com/articles/connecting-to-github-with-ssh/) for setting up SSH on Github.

#### Using HTTPS

If you want to use HTTPS, use the _personal access token as the password_ when you push. However, specifying the token as a password everytime is quite cumbersome (even with caching on). So save the token in a file called `~/.netrc` in the following format:

```
machine github.com
login nikhita
password <token>
protocol https

machine gist.github.com
login nikhita
password <token>
protocol https
```

This is saves your token in a plain text file which is not secure so encrypt it with gpg:

```shell
$ gpg --encrypt --armor --recipient <email> .netrc
$ git config --global credential.helper "netrc -f ~/.netrc.asc -v"
```

So now when you push over HTTPS, it won't ask you for the username and token.

<br>

## Pro Tip

SSH is far more secure than HTTPS for authentication. With HTTPS, if your username and password are seen or copied by someone, then that person has access to your entire account. As long as you look after your private key, SSH is more secure and convenient. Even if someone had access to your private key (for the love of all that is holy, please don't let this happen), you can log in to your Github account and delete any stolen keys.

SSH can be tunneled over HTTPS if the network you are on blocks the SSH port. A nice [tutorial](https://help.github.com/articles/using-ssh-over-the-https-port/) is available. Thanks to [Sachin Kamath](https://blog.sachinwrites.xyz/) for mentioning this!



