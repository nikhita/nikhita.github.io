---
layout: post
title: Installing Go from source
description: A simple guide to install multiple versions of Go on the same machine. Particularly useful while installing Go from source.
comments: true
keywords: multiple versions, golang, go, same, computer, machine, how to, install, source code, HEAD, source repo
---

I wanted to contribute to the Go source (the programming language itself) but that meant I needed to have two go versions on my machine - the one I am using currently (1.8.1) and the HEAD. This is a post explaining how to achieve that. Please note that I am on Linux and I am _not_ using gvm for installing Go.

## Get the source code

You need to get the Go source code first, of course. The Go team has excellent instructions [here](https://golang.org/doc/contribute.html). Essentially you need to checkout the source repo anywhere **outside your GOPATH**.

```bash
$ git clone https://go.googlesource.com/go
```

Next, you'll need to build this version of Go.

```bash
$ cd go/src && ./all.bash
```

## Oh no! Errors!

Sadly, for me, this lead to an error as shown below:

```bash
##### Building Go bootstrap tool.
cmd/dist
ERROR: Cannot find /home/nikhita/go1.4/bin/go.
Set $GOROOT_BOOTSTRAP to a working Go tree >= Go 1.4.
```

But hey, I was already on Go 1.8.1! So I needed to set `$GOROOT_BOOTSTRAP` environment variable to point to the Go 1.8.1 binary. This error occurs because it defaults to `$GOROOT` if not specified and my `$GOROOT` is also not set (since I don't have a custom installation). Oops.

The simple fix:

```bash
$ export GOROOT_BOOTSTRAP=/usr/local/go
```

Build the binary using `./all.bash` again. It should work now! :tada:

## Aliasing

You have two Go binaries installed on your machine now. Yay! But now what? How should you decide which version needs to be invoked when you run `go version`?

In my case, I had 1.8.1 installed already and it's binary was already in my `$PATH` so this was my **default** version. 

```bash
$ go version
go version go1.8.1 linux/amd64
```

To invoke your new, shiny Go binary from HEAD, you'll need to use `go/bin/go version` where you installed the source repo. It's better to alias this so that you won't have to repeat this every time. Add something like this in your .zshrc/.bashrc/what-have-you - `alias godev=/home/nikhita/go-dev/go/bin/go`. Now when you run:

```bash
$ godev version
go version devel +8ec7a39fec Sat Jun 24 00:54:01 2017 +0000 linux/amd64
```

Viola! :boom:

