---
title: Reslove the timezone on Arch Linux
id: 40
categories:
  - Arch Linux Tips
date: 2016-05-27 08:44:45
tags:
---

First, you should set your bios time correctly.
sudo pacman -S hwinfo
sudo hwclock --systohc --utc
sudo hwclock --systohc --localtime