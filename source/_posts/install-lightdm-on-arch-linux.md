---
title: Install lightdm on arch linux
id: 35
categories:
  - Arch Linux Tips
date: 2016-05-27 08:40:38
tags:
---

1, sudo pacman -S lightdm lightdm-gtk-greeter
2, sudo vim /etc/lightdm/lightdm.conf
add one line under: [Seat:*]
greeter-session=lightdm-gtk-greeter