---
layout: post
title:  "Swapping Control & Alt in Linux"
date:   2009-04-19 23:34:56 +0530
categories: tutorial
author:     vince
thumbnail: /images/linux.png
tags:
 - linux
 - xorg
---

More for my own reference and in preparation of me completely gutting my system, I'm posting the contents of my .xmodmaprc file which swaps the left control and alt-keys. This allows me to use my linux laptop more like I used my mac, with the command key. Many distributions now let you swap this from a setting but if yours doesn't here is how to go about it.

Feel free to copy the contents to a file called .xmodmaprc and run it using the xmodmap command:

    remove Control = Control_L
    remove Mod1 = Alt_L
    keysym Control_L = Alt_L
    keysym Alt_L = Control_L
    add Control = Control_L
    add Mod1 = Alt_L


```
xmodmap .xmodmaprc
```

Note that with some modern Desktop Environments like Gnome 3, you can use the Gnome Tweaks package and have the DE handle this for you.
