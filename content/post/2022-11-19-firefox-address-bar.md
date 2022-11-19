---
layout: post
title:  "Make Firefox address bar work like Chrome"
date:   2022-11-19 12:00:00 +0530
categories: tutorial
author:     vince
thumbnail: /images/firefox.png

featureImage: /images/posts/Firefox-Searchbar.png
featureImageAlt: 'FireFox Searchbar Settings'
featureImageCap: "Firefox's default settings for search don't solve the problem"
shareImage: /images/posts/Firefox-Searchbar.png

tags:
 - linux
 - firefox
---

I've been using Firefox as my main browser for a few years now. I like supporting an independent organization and have come to really appreciate the containers functionality which helps me segragate activity. One gripe I've had is that I much prefer the way Google Chrome handle's URL completion. When I'm in Chrome and I type `d` it automatically autocompletes to `https://www.discord.com/app` in the address bar.

By contrast, in Firefox typing the same thing autocompletes to `https://www.discord.com` even if I've got the full URL bookmarked and have the settings set to just look at my browsing history and bookmarks. It's be a small, but annoying problem for me.

I can't say when the change was made but I finally discovered the solution!

```
1 - Go to about:config
2 - search for autofill
3 - change browser.urlbar.autoFill.adaptiveHistory.enabled to true
4 - restart the browser
```

After following the above steps, it should work just like Chrome. Hope this helped make your Firefox experience a little better!
