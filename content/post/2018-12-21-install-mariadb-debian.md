---
layout: post
title:  "Install MariaDB in Debian Stretch"
date:   2018-12-21 16:00:00 +0530
categories: tutorial
author:     vince
image:      /images/posts/linux-image.jpg
tags:
 - linux
 - debian
 - mysql
 - mariadb
---

Note that this article for local installation of Maria DB or MySQL. It's intended to help you get up and running with the database locally and is not intended as a production tutorial. If you need to use either in a production environment, please contact a professional.

Step 1: update and install

```
sudo apt update
sudo apt upgrade
sudo apt install mariadb-server mariadb-client
```

Step 2: (Optional) Run the secure installation. Doesn't hurt to see the options for future reference.

```
sudo mysql_secure_installation
```

Step 3: allow running as root without a password:

```
sudo mysql -u root -p
```

From inside the database shell:

    use mysql;
    update user set plugin='mysql_native_password' where user='root';
    flush privileges;
    quit;

Step 4: Install development libraries (this is needed, for example, to install the ruby mysql2 gem)

```
sudo apt install libmariadbd-dev
```
