---
title: Install Freebsd on Arch Linux
id: 38
categories:
  - Linux System
date: 2016-05-27 08:44:09
tags:
---

1, Getting the Image File
$ axel -n 8 ftp://ftp.freebsd.org/pub/FreeBSD/snapshots/amd64/amd64/ISO-IMAGES/10.3/FreeBSD-10.3-STABLE-amd64-20160429-r298781-uefi-memstick.img

2, Write the Image
# dd if=FreeBSD-10.3-STABLE-amd64-20160429-r298781-uefi-memstick.img of=/dev/sdc bs=1M conv=sync

3, Restart your pc, and choose the USB stick to boot

4, It turns out a easy GUI to install it.Just do it step by step. You can see it on http://www.freebsd.org/doc/en_US.ISO8859-1/books/handbook/bsdinstall-pos...

5, Notice that when you allocate your disk space, don't forget to add a boot to the disk.