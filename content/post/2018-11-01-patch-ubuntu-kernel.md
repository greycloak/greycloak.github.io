---
layout: post
title:  "Patch the Ubuntu Kernel"
date:   2018-11-01 16:00:00 +0530
categories: tutorial
author:     vince
thumbnail: /images/ubuntu.png
tags:
 - linux
 - ubuntu
 - kernel
 - envyx360
---

I bought an HP Envy x360 and out of the box it works pretty well with linux. I've got Ubuntu 18.10 installed and have only had to tweak a couple of minor things. There is however, one big problem and that is the touch screen doesn't work. It might be the HP firmware (I am still figuring out how to update it in linux) but in the meantime, there is a [patch](https://bugzilla.kernel.org/show_bug.cgi?id=198715#c14) available. The question is how do we apply it? Let's find out.

The first thing you'll need to do is grab a bunch of dependencies. From your command line, let's install them:

```
sudo apt install build-essential git flex bison bc libssl-dev gawk libudev-dev ocl-icd-opencl-dev libpci-dev libelf-dev python2.7 libncurses-dev fakeroot kernel-wedge binfmt-support ksh lsscsi binfmt-support libpcre16-3 libpcre3-dev libpcre32-3 libpcrecpp0v5 libsepol1-dev libattr1-dev libblkid-dev libpcre16-3 libpcre3-dev libpcre32-3 libpcrecpp0v5 libselinux1-dev libsepol1-dev uuid-dev debugedit libarchive13 libdw1 liblua5.2-0 liblzo2-2 libnspr4 libnss3 librpm8 librpmbuild8 librpmio8 librpmsign8 rpm rpm-common rpm2cpio spl-dkms
```

In our example we're going to be applying this patch to the latest kernel which is currently 4.19.6 Let's clone it:

```
git clone --depth 1 --single-branch --branch v4.19.6 git://git.launchpad.net/~ubuntu-kernel-test/ubuntu/+source/linux/+git/mainline-crack v4.19.6
```

If you look at the [website directory](http://kernel.ubuntu.com/~kernel-ppa/mainline/v4.19.6/) in question, you'll see the 6 patch files we need. Let's change into the newly cloned 4.19.6 folder and grab them:

```
cd 4.19.6
wget http://kernel.ubuntu.com/~kernel-ppa/mainline/v4.19.6/0001-base-packaging.patch
wget http://kernel.ubuntu.com/~kernel-ppa/mainline/v4.19.6/0002-UBUNTU-SAUCE-add-vmlinux.strip-to-BOOT_TARGETS1-on-p.patch
wget http://kernel.ubuntu.com/~kernel-ppa/mainline/v4.19.6/0003-UBUNTU-SAUCE-tools-hv-lsvmbus-add-manual-page.patch
wget http://kernel.ubuntu.com/~kernel-ppa/mainline/v4.19.6/0004-debian-changelog.patch
wget http://kernel.ubuntu.com/~kernel-ppa/mainline/v4.19.6/0005-configs-based-on-Ubuntu-4.19.0-8.9.patch
```

We're next going to also grab the patch. Create a file in the same directory and let's called it x360.patch. Open up your favorite text editor and paste the [raw patch](https://bugzilla.kernel.org/attachment.cgi?id=275381) into it.

Time to start patching! From the command line:

```
patch -p1 < 0001-base-packaging.patch
patch -p1 < 0002-UBUNTU-SAUCE-add-vmlinux.strip-to-BOOT_TARGETS1-on-p.patch
patch -p1 < 0003-UBUNTU-SAUCE-tools-hv-lsvmbus-add-manual-page.patch
patch -p1 < 0004-debian-changelog.patch
patch -p1 < 0005-configs-based-on-Ubuntu-4.19.0-8.9.patch
patch -p1 < x360.patch
```

Note that the file names will probably change depending on the kernel version you are patching. With that done it's time to make the kernel config from current Kernel config:

```
yes "" | make oldconfig
```

And then, let's make the kernel!

```
make deb-pkg
```

This may take a while depending on your machine. If I recall correctly it took a couple of hours on my HP Envy x360. When it's finally done, you'll have a bunch of .deb files in the directory above. We need to install them:

```
cd ..
sudo dpkg -i linux*4.19*.deb
```

Finally, update grub and reboot:

```
sudo update-grub
sudo reboot
```

You can check you're on your new kernel by typing `uname -r` on the command line after reboot. Remember that if anything goes wrong, you haven't erased your old kernel. Hit `esc` on reboot to get to your grub prompt and then select your older kernel to try to resolve.

Happy patching!
