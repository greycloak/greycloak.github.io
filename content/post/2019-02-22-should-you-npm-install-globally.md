---
layout: post
title:  "Should you npm install globally?"
date:   2019-02-22 12:00:00 +0530
categories: tutorial
author:     vince
tags:
 - nodejs
 - npm
 - linux
---

I was transitioning this blog from using Jekyll to Hexo. After comparing both, I feel I made the right choice. However, I almost started off on the wrong foot. Being unfamiliar with Node.js, I was reviewing the Hexo install instructions and the first thing it tells you is to install via:

```
npm install hexo-cli -g
```

I'm running on Archlinux and got a permission denied error when I tried that. It's likely because I used pacman (the Archlinux package manager) to install node and/or npm. So that left me with the decision of whether to use sudo to force the install. After years of running homebrew, that felt like the wrong decision. And it is. Instead of using sudo, fix permissions or create a new directory. If in doubt, your problem is likely solved by creating a new, local directory.

The first step in diagnosing is figuring out where npm is storing its packages. To do that, I ran

```
npm config get prefix
```

and found that my directory was set to /usr. I didn't want to change the permissions of /usr so knew that I needed to switch the directory where the node packages are installed. To do that:

Step 1:  Make a directory for global installations:

```
mkdir ~/.npm-global
```

Step 2: Configure npm to use the new directory path:

```
npm config set prefix '~/.npm-global'
```


Step 3: Open or create a ~/.profile file and add this line:

```
export PATH=~/.npm-global/bin:$PATH
```

Step 4: Source that file so it uses the new path:

```
source ~/.profile
```

You should now be able to download and install the package with the -g flag without using sudo. Try the original hexo install command again:

```
npm install hexo-cli -g
```

HT to [this post](https://stackoverflow.com/questions/47252451/permission-denied-when-installing-npm-modules-in-osx) on Stack Overflow which had all the answers.

{{% notice info "tl;dr" %}}
* you shouldn't need sudo
* create a local directory instead and add it to your path
{{% /notice %}}
