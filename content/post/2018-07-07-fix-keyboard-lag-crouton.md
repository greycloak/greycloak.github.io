---
layout: post
title:  "Fixing keyboard and mouse lag in Xorg (crouton)"
date:   2018-07-07 03:34:56 +0530
categories: tutorial
author:     vince
image:      /images/posts/linux-image.jpg
tags:
 - chromeos
 - crouton
 - xorg
---

I've been using a Chromebook for development lately. On the side, I like to load up games and play using the linux installation I have loaded up via Crouton. [Crouton](https://github.com/dnschneid/crouton) is amazing and what we'll be using until native linux comes baked in, but it has some issues. There are a number of "targets" for displaying a desktop environment including xiwi and xorg. Here, I'll discuss those two targets and tell you how to fix performance in the latter.

The first target is **xiwi**. It essentially uses ChromeOS to manage the windows in whichever Desktop Environment you picked (e.g. XFCE). This allows some really neat tricks like launching an application inside a Chrome tab or separately without launching your full Desktop Environment. If I were just messing around in XFCE this would be my choice. Depending on how and the order in which you installed the crouton targets you might launch into XFCE just by typing:

```
sudo startxfce4 -X xiwi
```

The major problem with xiwi is that there's **no hardware acceleration**. You can check that by installing `mesa-utils` and running glxinfo or glxgears.

```
sudo apt install mesa-utils
glxinfo | grep vendor
```

You'll likely see *VMWare as the Vendor* which means we're emulating hardware acceleration. Just fine for watching videos but it's not going to cut it for most games. Running `glxgears` will likely show some decent FPS though.

Up next is **xorg**. This is going to launch xfce again but this time we're not relying on ChromeOS for anything. The good news here is that hardware acceleration works! The bad news is that there are some performance problems and also that your Chromebook Graphics Card is probably terrible anyway. I can't help with the latter. But let's try to fix some of those performance issues.

You might have a **laggy mouse**. To fix it temporarily, pop open the terminal and type:

```
synclient FingerLow=1 FingerHigh=5
```

If that fixed your trackpad issue then you can make it permanent on boot by creating a file at `/mnt/stateful_partition/crouton/chroots/xenial/etc/X11/Xsession.d/80synaptics` and entering the above info. The file would end up looking like:

    # Touchpad sensibility (move)
    synclient FingerLow=1
    synclient FingerHigh=5

For the *keyboard lag*, we'll take a nod from the solution presented in [this thread](https://github.com/dnschneid/crouton/issues/3491#issuecomment-396965306) by Adam and copy over the Intel SNA driver.

```
sudo cp  /etc/crouton/xorg-intel-sna.conf  /etc/X11/xorg.conf
```

Exit and re-enter your xorg xfce chroot and let's take a look at the same metrics. This time looking at glxinfo will show a *Vendor string of Intel*. And glxgears is going to match your screen refresh rate (probably 60fps). Congrats, you've now got hardware acceleration! You probably can't play anything too beefy but you'll have slightly better performance. If you're using Lutris, you might get dxvk enabled as well for an incremental gain.

Lastly, I should mention that I primarily use cli-extra to just work at the command line. I think this is the happy place for Crouton and where most people use it successfully. But regardless, I hope you find your chromebook useful!
