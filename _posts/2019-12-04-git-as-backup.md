---
layout: post
language: en
created: 2019-12-04 16:15:00 (CET)
title: Git as backup
tagline: a lost backup
description: Working without backup is scary, but what if even your backup is destroyed.
authors:
  - jeblad
categories :
  - other
tags:
  - git
  - backup
  - secure store
licenses:
  - CC-BY-SA-4.0
---

Some years ago I got a really weird phone call. I had worked on a project several years earlier, it was a project where code should not be taken outside the property, and they had lost their code. The call was rather frankly; did I take a copy outside the property, because (ehm) they had lost the code. Of course I did not have a copy, or rather I did not know about a copy at that time. How can you create a secure backup in a git development environment without to much hassle, and is it possible at all?

<!--more-->

{% include opinion.html %}

The same weird thing happen a few years later. I had written several extensions for [MediaWiki](https://en.wikipedia.org/wiki/MediaWiki) ([site](https://mediawiki.org)) and used a repository at the company where I was subcontracting. Then the company went bankrupt and the server was closed. Things like that happen. Even if the company went out of business, their customers still had my code, and could continue.

I was asked the same question a few months ago. These days I usually use [GitHub](https://en.wikipedia.org/wiki/GitHub) ([site](https://github.com)) as repository for whatever I do that is public. That usually work out pretty well. In April 2018 Microsoft acquired Github, and that was a bit chilling, what would now happen to the repositories. Thus I started to look for alternatives. I did not want just any repository, as I already have local backup, but I wanted to move important repositories to a secure off-site store. It is not that they are very scary in any sense, but accidents do happen, like in those previous calls.

For a time I used several ad-hoc solutions, also toying with storing encrypted files on [Dropbox](https://en.wikipedia.org/wiki/Dropbox_(service)) ([site](https://dropbox.com)) and [Google Drive](https://en.wikipedia.org/wiki/Google_Drive) ([site](https://drive.google.com)), but it doesn't really work, and it was definitely not seamless. I needed something better.

Then I stumbled upon [Keybase](https://en.wikipedia.org/wiki/Keybase) ([site](https://keybase.io)). At first I was only looking for a site with federated identity, but later they made available [git repositories](https://keybase.io/docs/git/index) that could be used both as private and team repo. The team repos are quite interesting, as Keybase also has extensive support for [teams](https://keybase.io/docs/teams/index). The private repos are although more interesting, as they makes it possible to create shadow repositories to my public repositories at GitHub. If the public repo at GitHub goes down for whatever reason the private repo at Keybase will still be available.

After installing `keybase` an shadow repository can be created

    keybase git create myrepo

Now you have an empty repo at keybase, but still has to point your existing repo to the external repo, so add a few lines to your `.git/config` like so

    pushurl = git@github.com:user/myrepo.git
    pushurl = keybase://private/user/myrepo

This is assuming your have `url = https://github.com/user/myrepo.git` for `remote "origin"`. I use https for most operations, but for push I use ssh, thus the `git@github…` stuff at the first line. I show this because I want to visualize that you can infact have two `pushurl` statements. The second line is the repo at Keybase, which use an other action during upload. From the outside this looks just like an ordinary `git push`, and even [Visual Studio Code](https://en.wikipedia.org/wiki/Visual_Studio_Code) sees nothing out of the ordinary and pushes gladly to the additional repo. Thus I now maintain a backup at Keybase while using a public repo at GitHub.

Editing the `.git/config` can be a little awkward, but you can do the same with

    git remote set-url origin --push --add git@github.com:user/myrepo.git
    git remote set-url origin --push --add keybase://private/user/myrepo

On the first push Keybase will initialize, and there will be some additional output.

A pull on this setup will get the commits on GitHub, while pushes will go to both GitHub and Keybase. Usually you will never see the Keybase repo, all work will be done on GitHub. You should not get a merge conflict on Keybase, but you can get a merge conflict on GitHub.

Last thing; make sure you have a secure storage for your login at both Keybase and GitHub, and preferably use a key management tool!
