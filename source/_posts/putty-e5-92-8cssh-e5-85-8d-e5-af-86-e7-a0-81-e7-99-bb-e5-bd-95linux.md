---
title: putty和ssh免密码登录linux
id: 30
categories:
  - Windows
date: 2016-05-26 17:55:01
tags:
---

1，windows putty
vim ~/.ssh/authorized_keys
put your public key in up file.
putty
puttgen.exe
2, linux ssh
ssh-keygen
ssh-copy-id user@server