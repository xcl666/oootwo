---
title: Install Gentoo on Arch Linux
id: 37
categories:
  - Linux System
date: 2016-05-27 08:41:39
tags:
---

You can see it on http://www.unixmen.com/a-beginners-guide-to-install-gentoo/ and http://showerlee.blog.51cto.com/2047005/1314053 .
Make sure you are the user of "root"!
1, Setting up Partitions
/dev/sdXX
mkfs.ext4 /dev/sdXX
mkdir /mnt/gentoo
mount /dev/sdXX /mnt/gentoo

2, Downloading and Extracting the Tarball
axel -n 8 http://distfiles.gentoo.org/releases/amd64/autobuilds/20160505/stage3-amd64-20160505.tar.bz2
cd /home/liv/Downloads
tar xvjpf stage3-*.tar.bz2 -C /mnt/gentoo
cd /mnt/gentoo
3, cp -L /etc/reslov.conf /mnt/gentoo/etc/
4, mount -t proc none /mnt/gentoo/proc
mount --rbind /sys /mnt/gentoo/sys
mount --rbind /dev /mnt/gentoo/dev
5, chroot /mnt/gentoo /bin/bash
source /etc/profile
export PS1="(chroot) $PS1"
5, nano /etc/portage/make.conf

# *** CFLAGS and CXXFLAGS ***
# CFLAGS and CXXFLAGS variables define the optimization flags for gcc C and C++ compiler.
# See https://wiki.gentoo.org/wiki/GCC_optimization for more information.
CFLAGS="-O2 -pipe -march=native"
CXXFLAGS="${CFLAGS}"
#
# *** CHOST ***
# WARNING: Changing your CHOST is not something that should be done lightly.
# Please consult http://www.gentoo.org/doc/en/change-chost.xml before changing.
# for 64bit Intel PCs
CHOST="x86_64-pc-linux-gnu"
# for 32bit Intel PCs
# CHOST="i686-pc-linux-gnu"
#
# *** USE flags ***
# These are the USE flags that were used in addition to what is provided by the
# profile used for building.
# See official Gentoo docs for more information.
USE="bindist mmx sse sse2 udev branding dbus startup-notification"
#
# *** MAKEOPTS ***
# With MAKEOPTS you define how many parallel compilations should occur
# when you install a package. A good choice is the number of CPUs (or CPU cores)
# in your system plus one, but this guideline isn't always perfect.
MAKEOPTS="-j7"
# The nuber "7" means the nuber of CPU+1, so if you have a dual core machine use -j3.
GENTOO_MIRRORS="http://mirror.bjtu.edu.cn/gentoo/"

6, emerge-webrsync
emerge --sync
if needed
emerge --oneshot portage

7, Choosing the Profile
eselect profile list
Available profile symlink targets:
[1] default/linux/amd64/13.0
[2] default/linux/amd64/13.0/selinux
[3] default/linux/amd64/13.0/desktop
[4] default/linux/amd64/13.0/desktop/gnome
[5] default/linux/amd64/13.0/desktop/kde
[6] default/linux/amd64/13.0/developer
[7] default/linux/amd64/13.0/no-multilib
[8] default/linux/amd64/13.0/x32
[9] hardened/linux/amd64
[10] hardened/linux/amd64/selinux
[11] hardened/linux/amd64/no-multilib
[12] hardened/linux/amd64/no-multilib/selinux
[13] hardened/linux/amd64/x32
[14] hardened/linux/uclibc/amd64
# eselect profile set 3

8, Setting up the Timezone
# ls /usr/share/zoneinfo
# cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
# echo "Asia/Shanghai" &gt; /etc/timezone

9, Choosing and Compiling Kernel
# emerge gentoo-sources
# cd /usr/src/linux
# make menuconfig

In this step, you should configure your kernel. The important is to make the your net work.
Device Drivers ---&gt; Network device support &gt; Ethernet drive support
Choose what driver which you use.

# make -j7 &amp;&amp; make modules_install
# make install
# emerge --ask sys-kernel/genkernel
# genkernel --install initramfs

10, # nano /etc/conf.d/hostname
hostname="your-hostname"

11, # nano /etc/locale.gen
en_US.UTF-8 UTF-8
# locale-gen
# nano /etc/env.d/02locale
LANG="en_US.UTF-8"
LC_COLLATE="C"
# env-update &amp;&amp; source /etc/profile

12, # vi /etc/conf.d/net
config_eno1=("192.168.168.0.2 netmask 255.255.255.0 brd 192.168.0.255")
routes_eno1=("default via 192.168.0.1")
# ln /etc/init.d/net.lo /etc/init.d/net.eno1
# rc-update add net.eno1 default

13, # passwd

14, # emerge --ask syslog-ng
# rc-update add syslog-ng default

15, Setting up /etc/fstab
# nano /etc/fstab
/dev/sdXX / ext4 noatime 0 1

16, # exit
pacman -S os-prober
grub-mkconfig -o /boot/grub/grub.cfg