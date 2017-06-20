---
layout: post
title: How to update VSCode on Linux
description: A simple guide to update VSCode on Linux using apt-get.
comments: true
keywords: vscode, visual studio code, linux, ubuntu, debian, update, upgrade, apt-get, apt, get, dpkg, website, without
---

Whenever VSCode makes a new version available, it prompts you to go to the website and manually download the deb package. But downloading the deb everytime there is an update...just sucks.

Luckily, Microsoft has introduced official signed repositories with the [February 2017 (v1.10)](https://code.visualstudio.com/updates/v1_10#_miscellaneous) update. So to update VSCode, you need to do the following:

```bash
$ sudo add-apt-repository -y "deb https://packages.microsoft.com/repos/vscode stable main "
$ sudo apt update
$ sudo apt -y install code
```

This will install the new version of VSCode with all your _old extensions still enabled_.

The next time a dialog box prompts you that there is a new version available, you don't need to do the above steps again. You can upgrade it using:

```bash
$ sudo apt-get update 
$ sudo apt-get dist-upgrade
```

Note: If you are unfamiliar with `dist-upgrade`, [this](https://askubuntu.com/questions/81585/what-is-dist-upgrade-and-why-does-it-upgrade-more-than-upgrade) might prove to be a good read.

After the update, reload the window. You should be welcomed with release notes for the new version. This means that the update was successful and you got it up and running! :tada: