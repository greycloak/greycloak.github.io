---
layout: post
title:  "Quick Tip: Set up a Reverse SSH Tunnel"
date:   2009-06-10 23:34:56 +0530
categories: tutorial
author:     vince
thumbnail: /images/linux.png
tags:
 - linux
 - ssh
---

Often times I find myself using ssh to get to a server in order to get a file. The problem is that my local machine doesn't have its own publicly accessible IP address. So I end up ssh'ing into the remote server, creating the file I need (e.g. database backup) and then exiting only to run scp from my local machine afterwards. Plus, if after that I want to erase the file on the remote server I have to ssh in again and tidy up after myself. That's me running ssh x2 and scp x1 every time I want to accomplish what should be simple. There's got to be an easier way, right? You bet..


First thing you'll want to do is ssh into your server but this time we're going to pass a -R flag and a port number. That flag "Specifies that the given port on the remote (server) host is to be forwarded to the given host and port on the local side." Basically a reverse tunnel..

```
ssh -R 19999:localhost:22 youruser@yourserver.com
```

Once you're in, you can ssh back to localhost:

```
ssh localhost -p 19999
```

or copy a file down:

```
scp -P19999 YOUR_FILE youruser@localhost:/home/youruser/
```

And that is all there is to it! Thanks due to HowTo Forge for pointing the way on this. They've got a bit more on the topic that you can [read about here](https://www.howtoforge.com/reverse-ssh-tunneling).
