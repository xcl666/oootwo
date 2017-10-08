---
title: 'arch: clean the cache and get the list of pakages you installed'
id: 31
categories:
  - Arch Linux Tips
date: 2016-05-26 17:56:38
tags:
---

commands: pacman -Scc
commands: LANG=C pacman -Sl | awk '/[installed]$ {print $1 "/" $2 "-" $3}' &gt; /home/xcl/pkglist.txt