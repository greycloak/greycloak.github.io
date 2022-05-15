---
layout: post
title:  "Quick Tip: Sort by directory size in linux"
date:   2009-02-14 23:34:56 +0530
categories: tutorial
author:     vince
thumbnail: /images/linux.png
tags:
 - linux
---

If you've got files hidden around your system and you don't know where they are, you can use a quick command to track them down and sort them with the largest first. Handy when trying to prune your old files or free up space on your hard disk.

Try this:

```
sudo du --max-depth=1 /home/ | sort -n -rs
```
