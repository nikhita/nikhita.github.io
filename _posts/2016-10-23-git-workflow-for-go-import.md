---
layout: post
title: Git workflow while working with Go
description: While working with go, it is easy to mess up your import path. Here's a git workflow which can set it right.
comments: true
image:
keywords: golang, gocode, git, workflow, import, path, mess, fork, update, generate
---

If you are writing code in Go and you want to contribute to some open source project, chances are you won't get it right on your first try if the project is using import paths referencing to the original import path ie. the import paths correspond to the original repo and not your fork!

## The Problem

I was working on [taskcluster-cli](https://github.com/taskcluster/taskcluster-cli). If you notice carefully, it has a file called `subtree-imports.go` which automatically imports _subtrees_, which means it has import paths like:

```
github.com/taskcluster/taskcluster-cli/apis
```
If I fork the project and automatically generate imports, it will import a path something like this:

```
github.com/nikinath/taskcluster-cli/apis
```

This is horribly screwed up now! :(

## The solution

Let's dive into the heart of the problem! The import paths get messed up because they depend on where the code is residing. When I clone my fork, the code is now residing at `$GOPATH/src/github.com/nikinath/taskcluster-cli ` and not at `$GOPATH/src/github.com/taskcluster/taskcluster-cli` which leads to...import hell?

So we see that the solution is to make sure that your code resides at `$GOPATH/src/github.com/taskcluster/taskcluster-cli`. Wait! Before you freak out and start yelling "I WANT TO PUSH TO MY FORK, NOT THE ORIGINAL REPO", let's add some more remotes! :D

### Get the names right!

If you do a `$ git remote -v` at the location where your original repo is, you'll probably see something like this:

{% highlight bash %}
origin    https://github.com/taskcluster/taskcluster-cli (fetch)
origin    https://github.com/taskcluster/taskcluster-cli (push)
{% endhighlight %}

Before I add more remotes, I want to get my naming right. Let's call this remote as _upstream_. Just do a `$ git remote rename origin upstream`.

For a sanity check, let's `$ git remote -v` again:

{% highlight bash %}
upstream    https://github.com/taskcluster/taskcluster-cli (fetch)
upstream    https://github.com/taskcluster/taskcluster-cli (push)
{% endhighlight %}

Phew, we are out of messing up with names now! :)

### Adding your fork

Now I'll add my fork as a remote. Let's call it _origin_.

{% highlight bash %}
$ git remote add origin https://github.com/nikinath/taskcluster-cli.git
{% endhighlight %}

We can see that doing this does us good:

* Now our import paths point to `$GOPATH/src/github.com/taskcluster/taskcluster-cli` and not a directory with my fork.
* My import paths will no longer get messy.
* I can still safely make changes and push to my fork (origin).

### Setting things right

Read this only if you have made some changes, pushed it to a remote repo (mostly your fork) and now realized that you have to sort out everything. If you a fresh fork, move onto the next section.

To fix this, you can create branches according to your fixes and make these branches track the branches in the remote fork.

1. Create a new branch according to your fix. Let's call the branch _my-fix-local_.
2. If you have previously worked on the fix and pushed it to your forked repo, make the local branch track your remote branch.
3. Pull your work from the remote branch

{% highlight bash %}
# create a new branch
$ git checkout -b my-fix-local
$ git checkout master
# list all branches
$ git branch
# track the local branch with the remote branch
$ git branch --track my-fix-local origin/my-fix-remote
# get your work back!
$ git pull
{% endhighlight %}


{% highlight javascript %}
function demo(string, times) {
  for (var i = 0; i < times; i++) {
    console.log(string);
  }
}
demo("hello, world!", 10);
{% endhighlight %}



### Check the import paths

Now that you have your repo in the right location, with the changes you had made, you can import all your paths again. This time, you'll see that there would be no conflicts with original import paths and all's good! :)

### Let's push it!

* Import paths in order? Check.
* Changes present? Check.
* My fork as a remote? Check.

Great, we have everything set up right - let's push it now! :)

{% highlight bash %}
# if you are not already on the branch
$ git checkout my-fix-local
$ git push
{% endhighlight %}

Simple!

For sending a pull request, you can use Github.

### Updating your repo

While you were busy sorting out your import paths, someone else might have contributed some code. To update your repo, you can fetch and merge.

{% highlight bash %}
$ git fetch upstream
$ git checkout master
$ git merge upstream/master
{% endhighlight %}

I generally don't like touching `rebase` unless necessary but you could also do a `git rebase upstream/master`.

## Closing note

Finally...we are done!

If you have any suggestions or constructive criticism, feel free to drop them in the comments section or mail me at nikitaraghunath@gmail.com.

PS: I am a Go newbie so if there is something wrong, please tell me - I'd love to improve! :)
