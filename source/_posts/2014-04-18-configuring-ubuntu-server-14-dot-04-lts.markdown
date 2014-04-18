---
layout: post
title: "Configuring Ubuntu Server 14.04 LTS"
date: 2014-04-18 17:27:00 +0700
comments: true
categories: [ubuntu, learning]
---
Objective: Install and configure

	*	SSH Server
	* 	Java JDK


1. Install and configure SSH
``` 
$ sudo apt-get install openssh-server
```

Setup SSH certificate
```
scp ~/.ssh/id_rsa.pub <username>@<host>:~/.ssh/authorized_keys
```

2. Install and configure Java JDK

```
$ sudo apt-get install openjdk-7-jdk

$ java -version
java version "1.7.0_51"
OpenJDK Runtime Environment (IcedTea 2.4.6) (7u51-2.4.6-1ubuntu4)
OpenJDK 64-Bit Server VM (build 24.51-b03, mixed mode)
```
