---
title: How to Install JAVA 8 (JDK/JRE 8u131) on Debian 8 & 7 via PPA
id: 52
categories:
  - Linux Server
date: 2017-08-17 14:05:00
tags:
---

Install Java 8 on Debian 8 And 7\. The first Oracle Java 8 stable version was released on Mar 18, 2014 and available to download and install. Oracle Java PPA for Debian systems is being maintained by Webupd8 Team. JAVA 8 is released with many of new features and security updates. Ubuntu and LinuxMint users use below link to install Java 8 on their system.

How to Install Java 8 on Ubuntu &amp; LinuxMint
How to Install Java 8 on CentOS, RHEL &amp; Fedora
This article will help you to Upgrade/Install Java 8 on Debian 8/7 system using PPA or Apt-Get command line package manager.

1\. Add Java 8 PPA

First, you need to add webupd8team Java PPA repository in your system. Edit a new PPA file /etc/apt/sources.list.d/java-8-debian.list in text editor

$ sudo vim /etc/apt/sources.list.d/java-8-debian.list
and add following content in it.

deb http://ppa.launchpad.net/webupd8team/java/ubuntu trusty main
deb-src http://ppa.launchpad.net/webupd8team/java/ubuntu trusty main
Now import GPG key on your system for validating packages before installing them.

$ sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys EEA14886
2\. Install Java 8 on Debian

Now use the following commands to update apt cache and then install Java 8 on your Debian system.

$ sudo apt-get update
$ sudo apt-get install oracle-java8-installer
3\. Verify Java Version

Finally, you have successfully installed Oracle Java on your Debian system. Let’s use the following command to verify installed version of Java on your system.

rahul@tecadmin:~$ java -version

java version "1.8.0_131"
Java(TM) SE Runtime Environment (build 1.8.0_131-b11)
Java HotSpot(TM) 64-Bit Server VM (build 25.131-b11, mixed mode)
4\. Configure Java Environment

In Webupd8 PPA repository also providing a package to set environment variables, Install this package using the following command.

$ sudo apt-get install oracle-java8-set-default
References:
https://launchpad.net/~webupd8team/+archive/java

From : https://tecadmin.net/install-java-8-on-debian/

&nbsp;