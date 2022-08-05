---
layout: post
title:  "Joplin CLI on Raspberry Pi 4"
date:   2022-08-05 12:00:00 +0530
categories: blog
author:     vince
thumbnail: /images/terminal-icon.png

featureImage: https://joplinapp.org/images/ScreenshotTerminal.png
featureImageAlt: 'Joplin'

tags:
 - linux
 - raspberrypi
 - manjaro
---

I've been searching for a way to keep my notes and todos organized. Over the years I've tried some interesting solutions like Evernote, Google Tasks, and even Task Warrior. All of them have their pros and cons but I've recently really liked the flexibility and ease of use of [Joplin](https://joplinapp.org/).

The screenshots will show you that it's got a complete Graphical User Interface and is usable across most operating systems including Linux so if you want to do that, by all means check it out. Installation is pretty straight forward and you won't need this guide.

However, if you prefer to use the terminal like I do, Joplin also comes with a command line interface which you can use to create, edit, delete notes and todos using a familiar interface. You can even use your editor of choice and customize the keybindings.

I recently got myself a Raspberry Pi 4 model B and decided to install Joplin. I'm using it headless so I only want the CLI. Joplin does support this but if you're on Manjaro like I am you'll need to install a few packages first.

    $ sudo pacman -S base-devel libheif libjxl rsync jq libgsf libvips openjpeg2 yq lcms2 openslide poppler-glib imagemagick

Now you've got the basics, go ahead and install nodejs. I prefer to do it using [nvm](https://github.com/nvm-sh/nvm). Their webpage has the install instructions and you should use those rather than copying a shell command from a blog. :)

Once nvm is install, go ahead and install node. I prefer the LTS version which you can install with

    $  nvm install --lts

Lastly, you should be ready to go with Joplin. Their [webpage](https://joplinapp.org/terminal/) also has the commands so check there for updates but it's as simple as:

    NPM_CONFIG_PREFIX=~/.joplin-bin npm install -g joplin
    sudo ln -s ~/.joplin-bin/bin/joplin /usr/bin/joplin

Keep in mind you may need to reload your terminal to launch it, but you should be good to go.


If you're a vim user like me, keep in mind you can customize the keybindings. The only one I find a little annoying is that quitting Joplin itself is done with `q` instead of `:q` but hopefully that can get addressed at some point. I've forked the keybindings I use and you see the [gist here](https://gist.github.com/vince/dfe3fb3230f92eccf7d57f530afbd34c). Simply put that file in `~/.config/joplin/keymap.json` and restart.
