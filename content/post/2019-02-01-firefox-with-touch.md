---
layout: post
title:  "Getting touchscreen events working with Firefox"
date:   2019-02-01 12:00:00 +0530
categories: tutorial
author:     vince
thumbnail: /images/firefox.png
tags:
 - linux
 - firefox
---

I bought this laptop with a touchscreen and occasionally find myself using it while surfing websites. Now with Chrome that worked just fine but with Firefox it tends to select areas of text instead of scrolling. That sucks!

Fortunately it's quite fixable. You just have to modify the .desktop file (or launch from the command line) with an additional environmental option: `env MOZ_USE_XINPUT2=1`

On most linux distributions, the .desktop file is in `/usr/local/share/applications` or `~/.local/share/applications` but you can also modify it globally in `/usr/share/applications` if you have root.

```
vim ~/.local/share/applications/firefoxtouch.desktop
```

Then modify the Exec line so it looks like this instead:


    Exec=env MOZ_USE_XINPUT2=1 /usr/bin/firefox %u

If you're creating an entry from scratch in your local share directory you may want to give it a different name like "Firefox Touch"

```
[Desktop Entry]
Name=Firefox Touch
Comment=Browse the Web Touch
Icon=firefox
Exec=env MOZ_USE_XINPUT2=1 /usr/bin/firefox
Terminal=false
Type=Application
Categories=Network;WebBrowser;
StartupNotify=true
```

When you relaunch Firefox, you should have the ability to use your touchscreen in the same way Chrome uses it. If not, go back to your file and make sure you've modified ALL the entries.. sometimes the .desktop file has multiple ones for private browser, new window, etc. Hopefully Firefox makes this the default in the future but as of version 65, I'm still waiting.

{{% notice info "tl;dr" %}}
* modify or create .desktop file to add env MOZ_USE_XINPUT2=1
* file can be modified globally or created locally
* careful as there may be multipe Exec entries!
{{% /notice %}}
