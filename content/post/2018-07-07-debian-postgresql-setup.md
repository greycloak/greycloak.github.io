---
layout: post
title:  "Setting up PostgreSQL on Debian Buster"
date:   2018-07-07 03:34:56 +0530
categories: tutorial
author:     vince
thumbnail: /images/linux.png
tags:
 - debian
 - postgresql
---

In a previous article, we set up your Debian Buster system with git, ruby, and a bash shell that tells you the ruby version and branch. Next up, we're going to install PostgreSQL and dependencies needed to get it working with Ruby on Rails.

First, let's make sure your system is up to date:

```
sudo apt update
sudo apt upgrade
```

Next, we're going to jump right in and install postgres 10:

```
sudo apt install postgresql postgresql-contrib libpq-dev
```

Next, start it up:

```
sudo service postgresql start
```

Switch over to the postgres account on your server to continue setup by typing:

```
sudo -i -u postgres
```

Once there, we'll create a new role with your user. Since this is intended for local development we're going to make some easy assumptions.  In my case, I named the user with the same name as my debian username (vince) and made it a superuser as well.  If you're try to set up a server for production, this is probably not what you want to do.

    (debian)postgres@localhost:~$ createuser --interactive
    (debian)postgres@localhost:~$ exit

Since we're getting set up for LOCAL development, we're going to change some of the safeguards that PostgreSQL comes enabled with by default on Linux. Head over to /etc/postgresql/10/main/ and edit the `pg_hba.conf` file:

```
sudo vi /etc/postgresql/10/main/pg_hba.conf
```

Look for the entries that say `peer` or `md5` and change them to `trust`. Again, **DO NOT DO THIS FOR PRODUCTION**.

    # Database administrative login by Unix domain socket
    local   all             postgres                                trust

    # TYPE  DATABASE        USER            ADDRESS                 METHOD

    # "local" is for Unix domain socket connections only
    local   all             all                                     trust
    # IPv4 local connections:
    host    all             all             127.0.0.1/32            trust
    # IPv6 local connections:
    host    all             all             ::1/128                 trust
    # Allow replication connections from localhost, by a user with the
    # replication privilege.
    local   replication     all                                     trust
    host    replication     all             127.0.0.1/32            trust
    host    replication     all             ::1/128                 trust

Now that we're done with that, let's stop and start postgres

```
sudo service postgresql restart
```
