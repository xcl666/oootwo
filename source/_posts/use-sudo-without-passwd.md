---
title: use sudo without passwd
id: 12
categories:
  - Base Linux/Unix System Environment
date: 2016-05-26 17:55:33
tags:
---

file: /etc/sudoers or command: sudo visudo
add text: user ALL=NOPASSWD : ALL
sudo VISUAL=vim visudo
or
sudo EDITOR=vim visudo