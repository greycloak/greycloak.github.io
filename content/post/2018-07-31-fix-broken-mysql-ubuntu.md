---
layout: post
title:  "Reinstall a broken MySQL 5.7 Ubuntu Xenial"
date:   2018-07-31 10:34:56 +0530
categories: tutorial
author:     vince
thumbnail: /images/mysql.png
tags:
 - linux
 - ubuntu
 - mysql
---

I've noticed that particularly in Ubuntu Xenial, an apt-upgrade to mysql 5.7 fails. A standard re-install doesn't work for me so I've resorted to more extreme methods to get my install working. This is only suitable for development, mind you. Please do not attempt in production without full backups and supervision.

Error:

<pre>
Setting up mysql-server-5.7 (5.7.12-0ubuntu1) ...
Job for mysql.service failed because the control process exited with error code. See "systemctl status mysql.service" and "journalctl -xe" for details.
invoke-rc.d: initscript mysql, action "start" failed.
dpkg: error processing package mysql-server-5.7 (--configure):
 subprocess installed post-installation script returned error exit status 1
 Errors were encountered while processing:
  mysql-server-5.7
  E: Sub-process /usr/bin/dpkg returned an error code (1)
</pre>

Trying to remove and reinstall also fails. The only solution I've found so far is to completely purge MySQL and reinstall it from scratch. I'm sure you can tweak these instructions to backup and restore your data. Maybe if I swtich back from Postgres I'll be motivated to look that up but for now, restoring the one db that uses MySQL is pretty easy. So what's the process?

## 1. Remove MySQL

```
sudo apt purge mysql-server mysql-server-5.7
sudo apt purge mysql-server mysql-client mysql-common mysql-server-core-5.7 mysql-client-core-5.7
sudo rm -rfv /etc/mysql /var/lib/mysql
sudo apt autoremove
sudo apt autoclean
```

## 2. Reinstall MySQL

```
sudo apt update
sudo apt install mysql-server mysql-client --fix-broken --fix-missing
```


## 3. Restart MySQL

You'll have to re-enter all your passwords again but then you should be able to start up MySQL again:

```
sudo systemctl start mysql
```
