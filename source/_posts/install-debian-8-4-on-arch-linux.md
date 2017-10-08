---
title: Install Debian 8.4 on Arch Linux
id: 36
categories:
  - Linux System
date: 2016-05-27 08:41:08
tags:
---

You can see it on "https://www.debian.org/releases/stable/amd64/apds03.html.en"
Make sure your are using user "root".
1, mke2fs -j /dev/sdaX
mkdir /mnt/debinst
mount /dev/sdaX /mnt/debinst
2, pacman -S debootstrap
3, yaourt -S debian-archive-keyring
4, debootstrap --arch amd64 jessie /mnt/debinst http://mirror.bjtu.edu.cn/debian
or
debootstrap --arch amd64 jessie /mnt/debinst http://mirrors.163.com/debian
or
debootstrap --arch amd64 jessie /mnt/debinst http://ftp.us.debian.org/debian
5, LANG=C.UTF-8 chroot /mnt/debinst /bin/bash
apt-get install makedev
mount none /proc -t proc
cd /dev
MAKEDEV generic
6, vi /etc/fstab
/dev/sdaX / ext3 defaults 0 1
7, dpkg-reconfigure tzdata
8, vi /etc/network/interfaces
auto lo
iface lo inet loopback
auto eth0
iface eth0 inet dhcp

or

auto eth0
iface eth0 inet static
address 192.168.0.2
network 192.168.0.0
netmask 255.255.255.0
broadcast 192.168.0.255
gateway 192.168.0.1

9, vi /etc/resolv.conf
nameserver 192.168.0.1
10, vi /etc/hostname
yourhostname
11, vi /etc/apt/sources.list
deb-src http://mirror.bjtu.edu.cn/debian jessie main
deb-src http://ftp.us.debian.org/debian jessie main

deb http://security.debian.org/ jessie/updates main
deb-src http://security.debian.org/ jessie/updates main
12, apt install locales
dpkg-reconfigure locales
13, apt-cache search linux-image
apt install linux-image-arch-etc
14, exit
pacman -S os-prober
grub-mkconfig -o /boot/grub/grub.cfg