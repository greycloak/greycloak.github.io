---
layout: post
title:  "Fix Occasional Freezing on the HP Envy X360"
date:   2018-10-31 10:09:56 +0530
categories: tutorial
author:     vince
image:      /images/posts/linux-image.jpg
tags:
 - linux
 - ubuntu
 - envyx360
---
01/2019 update: This doesn't seem to be necessary with the 4.20 kernel!

I recently bought an HP Envy x360 13" with AMD Ryzen 5 and Vega 8 graphics.  I'll get into why another time but one of the things that didn't work quite well had to do with the laptop freezing every once in a while. It seemed random at first but some searching revealed that adding a kernel parameter solves the issue. That kernel param is `idle=nomwait`. Since it was successful in stopping the freezing, I thought I'd make it permanent. Here's how:

First a side note that if you need to get to the BIOS in the HP x360, you'll need to hit F10 on boot. Also, to get to the GRUB menu, you'll need to try escape. That assumes you went all in and wrote over your windows partition like I did. If you didn't then your boot options might be different.

Anyway, here we go:

```
gksudo gedit /etc/default/grub
```

Find the line starting with GRUB_CMDLINE_LINUX_DEFAULT and append idle=nomwait to the end.

    GRUB_CMDLINE_LINUX_DEFAULT="quiet splash idle=nomwait"

Next, run the following command:

```
sudo update-grub
```

On the next reboot, the kernel will be started with the new boot parameter. (To remove it, simply remove the parameter from `GRUB_CMDLINE_LINUX_DEFAULT` and run `sudo update-grub` again.

To verify your changes, you can see exactly what parameters your kernel booted with by executing:

```
cat /proc/cmdline
```
