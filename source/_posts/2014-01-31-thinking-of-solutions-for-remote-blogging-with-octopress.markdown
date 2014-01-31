---
layout: post
title: "Thinking of solutions for remote blogging with Octopress"
date: 2014-01-31 23:51:51 +0700
comments: true
categories: ["octopress","remote blogging"]
---
After done setting up blogging solution with Octopress, which is this blog is now powered by, I'm thinking of finding a solution to write blog post from iPhone. The first site came up from Google results is [this one](http://www.candlerblog.com/2012/04/01/remote-octopress-workflow). The solution seems very neat, it involves setting up a shared folder on Dropbox and a SSH server to run the Octopress flows. Setup a shared folder in Dropbox for holding git repository is easy part. The harder part is getting a always-on SSH server.

Currently I think of three solutions:

1. Make use of existing SmartTV box which is now running Android 4.2 to be a SSH server
1. Purchase a minimal VPS instance.
1. Purchase a Raspberry Pi and make it a SSH server

First solution is free because I already have one SmartTV box. However making Android box running RVM seems to be a difficult task. Further search, there is an attempt to [run a Linux distro on Android](http://forum.xda-developers.com/showthread.php?t=1585009). It looks promising and worth a try.

Second solution will cost at least 5$/month for a VPS instance. Which is not a good way to go at the moment.

Third solution will cost about 40$ and I'll got a Raspberry Pi for something else.

In conclusion, first solution goes first. If it is impossible to run RVM on Android box and come third solution.
