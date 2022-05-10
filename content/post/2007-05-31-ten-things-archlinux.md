---
layout: post
title:  "Ten Things I Love About ArchLinux"
date:   2007-05-31 10:34:56 +0530
categories: blog
author:     vince
image:      /images/posts/linux-image.jpg
tags:
 - archlinux
 - linux
---

I've been back on Mac OSX for over a year now, using it for all my daily activities from email and web surfing to programming and device syncing. Something has been eating at me though and I find myself pining for my old linux desktop. Since buying a new rig for kicks is out of the question, I instead dug up a beat up IBM T22 and grabbed my Kubuntu Alternative Install CD and went to it.

Unfortunately, Kubuntu didn't install in the two times I tried it. It's unusual and is probably a reflection of my hardware more than it is Ubuntu. Still, I had an itch to scratch and I was determined to get at it. Enter [Arch Linux](https://www.archlinux.org/). I've used Arch before and this article isn't about how it does on the Desktop or how well it installs. If you want to figure that out go find a review or, better yet, grab an ISO and install it yourself. (Arch installs nicely on VMWare Fusion BTW..)

After getting up and running with Arch again, I discovered there are things about it that I just absolutely love. Here are my top 10.


1.    It's fast. Yes, it's an i686 distro and while you might think that I'd grow impatient waiting for an application to launch on my aging 128MB RAM T22, you'd be wrong. It's actually quite snappy and I'm surprised. I've got both KDE and Fluxbox installed and they are both serviceable. Lack of bloat is a good thing.

2.    It's got a lean base. I recall a few years ago when I was overseas, I made a bad, stupid, mistake that ruined my linux install. I didn't bring a spare ISO with me but I needed to get work done. I had the choice of downloading a slew of distros but ended up grabbing Archlinux. The lean 140MB base CD downloaded in a few hours (slooow connections overseas back then) and installed in under 25 minutes. From there was I able to start downloading applications in one terminal while simultaneously working in the other.

3.    It's unbiased. KDE? Fluxbox? Gnome? Who cares! With Arch, you make the decisions so if you don't want something don't install it. If you want something, go grab it. Nothing is given more attention than the other and that's because the community has a varied user base with their own preferences. Somebody in there uses a similar setup to the one you're thinking about.

4.    The community. It's been said that some people use *nix because they hate Windows while other use *nix because they love Unix. (I've left the exact phrase vague for fear of starting a flame war.) I think I use Archlinux because I love linux and I think many in the Arch community feel the same way. The result is a strong, respectful community forum, a well documented wiki, and nice IRC Channel too.

5.    RC.CONF. Wait, you love Archlinux because of a file? Yes I do. Everything you need to mess with is in this file. Want to start a daemon on boot? Here you go. Want to eliminate a module from getting loaded? It's in there too. What about setting your IP address? Yup, it's covered. Overall, I find it lovely and I think many Arch users would agree.

6.    Pacman. Arch comes with a great, powerful package manager too. Unlike his peers, Pacman won't start installing packages without asking you first. What I mean by that is if you do a sudo apt-get install Foo, it'll go and do it. OTOH, if you type pacman -S Foo, you'll get a breakdown of what's being installed and then pacman will request permission to go ahead.

7.    It's a learning distro. Yeah, you need to know linux to really use it. Sure, it doesn't auto configure much. (In fact, sometimes I feel it screws up some things on purpose just to see if you're paying attention!) X11 won't work by default and neither will sound, suspend to ram, or much of anything else. But, it's all manageable thanks to the great community and documentation and you *will* learn a ton about linux while doing it. Much of that learning will stay with you no matter which distro you end up with.

8.    It rolls with it. Arch is a rolling distro so it's always up to date. Simply typing pacman -Syu will update your installation to the latest greatest everything. Sounds like a nightmare for a server but it's actually never let me down even after long periods of neglecting it. Still, I looove my install so I care and feed it daily. It blooms.

9.    It's current. With Arch, the packages are in the repository very quickly after they're released. Sometimes it doesn't become generally available (they *do* test) but if you want it you can enable the testing repository and help out with the bug hunt. Regardless, it's my experience that the versions of the packages in Arch are always further along. It's nice to have the latest greatest and it's also nice to know if a current version of a package fixes or adds a feature I'm interested in. If so, I'll take the time to compile it on the linux distro I use for my servers (Ubuntu).

10.    Ok, there's no number 10 and I lied.. this is just a Top 9. Sorry folks! Take a minute to suggest a 10th thing and maybe I'll append it to this list.

In any case, Arch isn't the only distro with the above great things and I obviously am not trying to imply that it's better than your favorite distro either. But, I do really enjoy it. A little later on I'll probably publish my list of 5 things I hate about Archlinux. But I'm only up to two at this point so it'll be a while until that list is fully compiled. Still, I'm sure some of you have suggestions for me. ;)
