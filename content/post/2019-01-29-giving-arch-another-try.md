---
layout: post
title:  "Giving Archlinux Another Try"
date:   2019-01-29 16:00:00 +0530
categories: blog
author:     vince
thumbnail: /images/ArchLinux.png
tags:
 - linux
 - archlinux
---

I bought an HP Envy x360 a few months ago. It had the right combination of features I wanted. Touchscreen, 360 flip, smaller screen size, and decent graphics chip.

The plan was I wanted to draw, read, and play games on a computer while running linux. Shouldn't be that hard to do but surpringly, any computers that have a touch screen and can flip are either too big to read on comfortably or have a lousy intel chip.

When I first got the x360 I wanted the easy way out so installed Ubuntu 18.10 on it. Sure enough most things worked. At that time the latest kernel was 4.19.1 so there were a few tweaks I had to make. One to [keep the laptop from freezing](https://hackido.com/2018/11/01/2018-11-01-patch-ubuntu-kernel/) and another to [patch the kernel](https://hackido.com/2018/11/01/2018-11-01-patch-ubuntu-kernel/) and allow me to use the touchscreen. But the rest mostly worked.. for a while.

By the time I'd upgraded to kernel 4.20 the laptop was no longer suspending properly. Further I had a lot of WiFi breakages. Dozens of searches and my own inquiries on forums could not solve either of those problems. Lastly, one of the last lingering problems was low FPS in my video games despite having upgraded to a newer 19.0 version of Mesa.

In the end, I had a choice. Go back to my Pixelbook or reinstall. I opted to reinstall and go with Arch again. Glad I did. [This tutorial](https://www.youtube.com/watch?v=dOXYZ8hKdmc) from Average Linux User was the most straight forward instructions I found. They're nearly flawless except he uses a wired Ethernet connection. `wifi-menu` ended up working for me so that wasn't a big deal.

When I was done, all my problems ended up going away. WiFi works (though I'm too lazy to figure out how to use NetworkManager for now and it conflicts with wifi-menu), my touchscreen doesn't need to be patched (due to newer kernel), suspend/resume is flawless, and the lag I had with the keyboard while playing Guild Wars 2 is gone. (FPS might be a tick higher too.. hard to confirm).

Overall, I'm really happy. I even took a vacation and was confident enough to bring only the Arch laptop with me. If you're not familiar with Arch Linux, I highly recommend you give it a try. A while back I wrote an article on why I like it so much. The good parts are still good although some things like rc.conf don't apply anymore. [Give it a read](https://hackido.com/2007/05/31/2007-05-31-ten-things-archlinux/) and then decide if Arch is right for you.

{{% notice info "tl;dr" %}}
* Lots of things didn't work in Ubuntu 18.10
* All those things work in Arch Linux
* Installation was made easy following a tutorial
* Happy to be using Arch Again!
{{% /notice %}}
