---
layout: post
title:  "Install Rmagick 3.1 on Archlinux"
date:   2019-04-16 12:00:00 +0530
categories: tutorial
author:     vince
tags:
 - archlinux
 - rmagick
 - ruby
---


So you're doing ruby development in 2019, eh? Good for you! Despite the rumors, Ruby on Rails is still a great way to get a project up and running. I managed to get the core of [https://www.rpgbuddy.com](https://www.rpgbuddy.com) up and running in a week. One of my clients is also still running Ruby and I need to upgrade them from an old 2.3.3 version to 2.6.2. With that I decided to update a bunch of old gems too. One of those is Rmagick.

I didn't have any problems with it on my Debian install. But on Arch I kept getting an error.

    checking for brew... no
    checking for gcc... yes
    checking for pkg-config... yes


    ERROR: Can't install RMagick 3.1.0. Can't find ImageMagick with pkg-config


    *** extconf.rb failed ***


Googling solutions always brought me back to a missing libmagickwand-dev for Debian/Ubuntu. Those packages don't exist on Arch so I was at a loss. Fortunately a while back I remember having a similar problem on Mac OS and recall the solution was to set the PKG_CONFIG path. Sure enough, that solves the problem here too:

```
export PKG_CONFIG_PATH=/usr/lib/imagemagick6/pkgconfig
```

After that installing the rmagick gem directly or via bundler would work just fine.

{{% notice info "tl;dr" %}}
* sudo pacman -S libmagick6
* PKG_CONFIG_PATH=/usr/lib/imagemagick6/pkgconfig bundle install
{{% /notice %}}
