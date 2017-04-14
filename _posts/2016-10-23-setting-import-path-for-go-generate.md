---
layout: post
title: Setting import path for go generate
description: Go generate can be used to automatically generate imports. But it is easy to mess it up. Here is what you could do to set it right.
comments: true
image:
keywords: golang, gocode, git, workflow, import, path, mess, fork, update, generate
---

Go generate is one of my favorite tools but it is easy to mess up the import paths if you are not careful. This problem generally occurs when the import paths end up referencing to _your_ fork and not to the _original_ repo. This is a very common issue if you are:

1. Using go generate
2. Collaborating with others over github (essentially having your own fork of the project)

## The Problem

I was working on [taskcluster-cli](https://github.com/taskcluster/taskcluster-cli). If you notice carefully, it has a file called `subtree-imports.go` which automatically imports _subtrees_ on running `go generate`, which means it has import paths like:

```
github.com/taskcluster/taskcluster-cli/apis
```

If I fork the project and automatically generate imports, it will import a path something like this:

```
github.com/nikhita/taskcluster-cli/apis
```

As you can see, the import path generated are different. This is all horribly screwed up now! :(

## The solution

Let's dive into the heart of the problem! The import paths get messed up because they depend on where the code is residing. When I clone my fork, the code is now residing at `$GOPATH/src/github.com/nikhita/taskcluster-cli ` and not at `$GOPATH/src/github.com/taskcluster/taskcluster-cli` which leads to...import hell?

So the solution is to make sure that your code resides at `$GOPATH/src/github.com/taskcluster/taskcluster-cli`. Wait! Before you freak out and start yelling "I WANT TO MAKE CHANGES AND PUSH TO MY FORK, NOT THE ORIGINAL REPO!", let's add some more remotes! :D

### Get the names right

If you do a `$ git remote -v` at the location where your original repo is, you'll probably see something like this:

{% highlight bash %}
origin    https://github.com/taskcluster/taskcluster-cli (fetch)
origin    https://github.com/taskcluster/taskcluster-cli (push)
{% endhighlight %}

Before adding more remotes, let's name everything how it should be. Let's call this remote as _upstream_. Just do a `$ git remote rename origin upstream`.

For a sanity check, let's `$ git remote -v` again:

{% highlight bash %}
upstream    https://github.com/taskcluster/taskcluster-cli (fetch)
upstream    https://github.com/taskcluster/taskcluster-cli (push)
{% endhighlight %}

Phew, we are out of messing up with names now! :)

### Adding your fork

Now I'll add my fork as a remote. Let's call it _origin_.

{% highlight bash %}
$ git remote add origin https://github.com/nikhita/taskcluster-cli.git
{% endhighlight %}

We can see that doing this does us good:

* Now our import paths point to `$GOPATH/src/github.com/taskcluster/taskcluster-cli` and not a directory with my fork.
* My import paths will no longer get messy.
* I can still safely make changes and push to my fork (origin).

### Fixing branches

Read this only if you don't have a fresh fork i.e. you have made some changes, pushed it to a remote repo (mostly your fork) and now realized that you have to sort out everything. If you a fresh fork, move onto the next section.

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

### Check the import paths

Now that you have your repo in the right location, with the changes you had made, you can import all your paths again. This time, you'll see that there would be no conflicts with original import paths and all's good! :)

{% highlight bash %}
$ go generate
{% endhighlight %}


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

While you were busy sorting out your import paths, someone else might have contributed some code. To update your repo, you can fetch and merge. I generally don't like touching `rebase` unless necessary but you could also do a `git rebase upstream/master`.

{% highlight bash %}
$ git fetch upstream
$ git checkout master
$ git merge upstream/master
{% endhighlight %}


And...we are done! :)
