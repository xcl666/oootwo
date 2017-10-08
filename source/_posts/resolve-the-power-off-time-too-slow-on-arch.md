---
title: Resolve the Power off time too slow on Arch
id: 39
categories:
  - Arch Linux Tips
date: 2016-05-27 08:44:31
tags:
---

sudo vim /etc/systemd/system.conf
Change
#DefaultTimeoutStopSec=90s
To
DefaultTimeoutStopSec=10s

sudo systemctl daemon-reload