---
layout: post
title:  "Setting up Debian Buster for Ruby Development"
date:   2018-07-06 23:34:56 +0530
categories: tutorial
author:     vince
thumbnail: /images/ruby.png
tags:
 - debian
 - ruby
 - git
---

So you've got a new debian install and need to get it set up to do real work? Here's a quick guide to get the packages you need assuming you're using Debian's current testing distro, `Buster`, installed.

First, let's make sure your system is up to date:

```
sudo apt update
sudo apt upgrade
```

Next, let's grab the essentials including git:

```
sudo apt install git curl zlib1g-dev build-essential libssl-dev libreadline-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt1-dev libcurl4-openssl-dev software-properties-common libffi-dev nodejs
```

Before we get too far, let's configure git. I'm going to assume you're going to do most of your fetching and pushing using https rather than ssh. And if not, that you'll follow other instructions to set up ssh.

```
git config --global color.ui true
git config --global user.name "YOUR NAME"
git config --global user.email "YOUR@EMAIL.com"
```

Next, let's get ruby installed. We'll use RVM

```
sudo apt install libgdbm-dev libncurses5-dev automake libtool bison
gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
curl -sSL https://get.rvm.io | bash -s stable
source ~/.rvm/scripts/rvm
rvm install 2.6.0
rvm use 2.6.0 --default
ruby -v
```

We've now got ruby installed and git installed. Let's tie them both together with a bash prompt that will tell us the ruby version and branch of any repo we're working in.

```
cd ~
curl -o ~/.git-prompt.sh \
  https://raw.githubusercontent.com/git/git/master/contrib/completion/git-prompt.sh
```

and then add the following to your ~/.bash_profile

     source ~/.git-prompt.sh

With that downloaded, add the following to your ~/.bashrc file

    export PS1=$'$(ruby -e "print RUBY_VERSION") \e[36m\u\e[0m\e[32m@\h\e[0m \e[33m \W\e[31m$(__git_ps1 " (%s)")\e[0m '
    export PS1="\[\033[G\]$PS1"

Source both files:

```
source ~/.bash_profile
source ~/.bashrc
```

With that done, next time you change into your git repo directory you'll have a pretty bash prompt that reminds you which version of ruby you're using along with the branch you are on. Next up, we'll take a look at setting up postgresql on Buster.
