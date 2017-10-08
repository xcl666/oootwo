---
title: wireless card
id: 34
categories:
  - Arch Linux Tips
date: 2016-05-27 08:40:10
tags:
---

Wireless Card

Install wifi utilities: pacman -S iw wpa_supplicant dialog wpa_actiond;

List wireless card status: iwconfig;

Scan and Connect to hot point: sudo wifi-menu

Remember this hot point for auto-connection later (modify the wireless name based on your machine): systemctl enable netctl-auto@wlp5s0.service