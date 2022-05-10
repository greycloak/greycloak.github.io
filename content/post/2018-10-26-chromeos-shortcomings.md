---
layout: post
title:  "ChromeOS Shortcomings"
date:   2018-10-26 10:09:56 +0530
categories: blog
author:     vince
image:      /images/posts/linux-image.jpg
tags:
 - linux
 - chromeos
 - pixelbook
---

I've been using ChromeOS as my main development machine for a while now. At first I logged in under my personal gmail and used Crouton for development, but after Crostini I decided to separate out my work and personal items. Here are a few things that still bother me and why I might go back to a full linux environment:


## Multiple Users - sign out
There are two major problems with multiple users on Chrome. The first is that once you sign in another user, you can't just sign them out. You have to sign out ALL users. This is incredibly annoying because of resources taken keeping another user signed in but also because of the lock screen privacy (see below).

## Multiple Users - order matters
When I'm logged in first as my work user, if I then sign in with my personal account, I can't access any of the android apps that I have installed under my personal account. Instead, it looks to my work account and see if the app I'm trying to launch is installed there. If not, I'm prompted to install it by the store.

Likewise, if I'm logged into my personal account first, things that are installed by my work user aren't accessible even when I log in there second. My entire linux installation (Crostini) will not launch. I have to sign out all users, sign in again as my work user first and then access the linux container.

This is a productivity killer as well.

## Development - keyboard mappings
With most Operating Systems you can configure the keyboard to work like you do. ChromeOS gives you basic options to swap your Alt and Control but there's not much more. For example if you don't like the keybinding to swap between open windows or want to map the assistant key to something else, you are out of luck. Developers are finicky.. we are worried about coding and sometimes muscle memory ends up distracting from our thoughts and costing us productivity. I'm really surprised nobody at Google has complained about this.


## Development - changing your crostini username
As of October 2018, Crouton still runs circles around Crostini. You have so much more flexibility. One of those areas is simply in setting your username. By default, Crostini assigns a username that's the same as the account name for your gmail. Now, you can do this with Crostini as well. From Crosh:

    crosh> vmc start termina
    (termina) chronos@localhost ~ $ run_container.sh --container_name penguin --shell --user username

The problem is that the files app's sidebar that says "Linux Files" will not work. It's still looking for your ssh file share. Now, you can fix that too:

    <ctrl> + <alt> + t
    vmc list
    vmc start termina
    lxc list
    lxc exec penguin -- /bin/login -f user.name

    $ sudo bash
    $ rm /etc/ssh/sshd_not_to_be_run
    $ systemctl restart sshd
    $ ln -s /home/user.name /home/username

But at some point, when Crostini gets an upgrade, things are probably going to break again. Essentially just to use your name for Crostini's instance you'll be doing as much work as you might running linux.

## Development - launching crostini in a tab
After you install Crostini, you get a shiny new terminal application. It works well enough. It doesn't support tabs but you can install another terminal app like [Tilix](https://gnunn1.github.io/tilix-web/) which will handle things wonderfully for you. Since there are no multiple desktops, I use chrome tabs to switch between my console and IDE. Launching Crostini in a tab is a slow process though:

1. Open crosh
2. vmc start termina
3. run_container.sh --container_name penguin --shell --user username

It's a lot to type. Sadly there's no bash history in termina nor does it allow for an alias to be created to quickly launch the linux container. Minor but yet another productivity killer.

## Development - sharing files from outside the shell
From the files app you can copy things to the linux container with a copy/paste or cut/paste. But things can't be done currently using the command line. Again, annoying. In Crouton the Downloads folder was shared so if you downloaded a large file you'll only have to change directory or move it  over before you interact with it.

## Security - tainted clipboards
Did you know all your signed in users share the same clipboard? I've been copying and pasting from my personal account and pasting into this editor which is running on my work account. Ouch.

## Security - Can't hide usernames on chromeOS lock screen
Google does give you the choice to hide screen names on login. This is great because somebody finding your chromebook and turning it on won't have an idea what email or username to try to break in. Things change dramatically if you put your chromebook to sleep though.

On resume, the chromebook displays a list of all users currently signed in. This includes their name, picture, and email address. I honestly don't understand how this hasn't been addressed either. If nothing else the same settings for the login screen should apply here. It's just sloppy that it doesn't.

There are of course plenty of good things to appreciate about using ChromeOS for development. The ability to backup your entire linux instance is really handy and makes experimenting easy. Also, although audio and graphics acceleration aren't here yet, they will be coming eventually. None of the hassles around sleep resume or bad drivers plague your experience. You can really see how most of the gripes above are minor and could be fixed without too much complexity. The exception might be the login sequence creating resource issues but once Android becomes less important to the ecosystem, I'm sure that could be addressed as well.
