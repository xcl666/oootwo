---
title: How to upgrade Debian 8 Jessie to Debian 9 Stretch
id: 55
categories:
  - Linux Server
date: 2017-08-21 11:59:04
tags:
---

Objective

This article explains a system upgrade procedure from Debian 8 Jessie Linux to Debian 9 Stretch.
What's New

Apart from the up to date Linux kernel, Stretch comes with a considerable amount of new and updated software as well as a number of packages had been rendered obsolete:

This new release of Debian again comes with a lot more software than its predecessor jessie; the distribution includes over 15346 new packages, for a total of over 51687 packages. Most of the software in the distribution has been updated: over 29859 software packages (this is 57% of all packages in jessie). Also, a significant number of packages (over 6739, 13% of the packages in jessie) have for various reasons been removed from the distribution.
SOURCE: debian.org
Preparations

Given that the Debian is an extremely robust Linux distribution, combined with the fact that there is nothing certain in life, the chances are, that after the upgrade you may end up with a broken system. Therefore, it is necessary to point out that no system upgrade is bulletproof and you should discuss, prepare and possibly test any proper failover or recovery process prior the proposed system upgrade to Debian Stretch. The rule of thumb is, the less software installed on your system, the higher chance for a successful upgrade.

The chances for a successful and fully functional upgrade are decreased by a number of 3rd-party packages installed on your current system. From this reason, remove any obsolete standard repository and 3rd-party software before you attempt the upgrade. The command which might be helpful here is:
# aptitude search '~o'
The above command will list all packages which are no longer in a standard repository list since they were removed; thus they were rendered obsolete, or the packages were installed manually.

Perform a full backup of data and manual configuration files residing on your current system. For example, these may include but not limited to user home directories, databases, websites, etc. In case you run Debian Linux virtually take a snapshot just in case something goes wrong during the Stretch upgrade.

Warning: MariaDB replaces MySQL database in Debian 9 Stretch. This introduces a new database binary data file format which is not backwards compatible with your current ( Debian 8 Jessie ) database format. During the upgrade your databases will be upgraded automatically. However, when you run into some issues during or after the upgrade, you will not be able revert back! From this reason it is important to backup all your current databases before you proceed with a Debian 9 Stretch upgrade!
REFERENCE: debian.org
Jessie Full Upgrade

Before we move on with the upgrade, let's fully upgrade our current Debian Jessie system:
# apt-get update
# apt-get upgrade
# apt-get dist-upgrade
If everything went smoothly, perform database sanity and consistency checks for partially installed, missing and obsolete packages:
# dpkg -C
If no issues are reported, check what packages are held back:
# apt-mark showhold
Packages On Hold will not be upgraded, which may cause inconsistencies after Stretch upgrade. Before you move to the next part, it is recommended to fix all issues produced by both above commands.
Update Package Repository to Debian Stretch

Now, that we have a current system fully upgraded, it is time to resynchronize the package index files with new Debian Stretch sources. This is done by editing /etc/apt/sources.list file to include Debian stretch package repository. First, make a backup the current /etc/apt/sources.list:
# cp /etc/apt/sources.list /etc/apt/sources.list_backup
Execute apt edit-sources or use your favourite text editor e.g., VIM to modify a current /etc/apt/sources.list file to include stretch repositories. Simply update keyword jessie to stretch.

Example:
FROM JESSIE
deb http://httpredir.debian.org/debian jessie main
deb http://httpredir.debian.org/debian jessie-updates main
deb http://security.debian.org jessie/updates main
TO STRETCH
deb http://httpredir.debian.org/debian stretch main
deb http://httpredir.debian.org/debian stretch-updates main
deb http://security.debian.org stretch/updates main
Alternatively, use a sed command to automate this tedious task:
# sed -i 's/jessie/stretch/g' /etc/apt/sources.list
Once the above /etc/apt/sources.list file edit is completed, use apt-get command to update packages index:
# apt-get update
Upgrade to Debian Stretch Simulation

Before we hit the UPGRADE button, let's use apt command to see a preview of what we are facing. To do this execute apt list --upgradable command in order to get a quick survey of the number of packages to be installed, updated and removed without affecting the system.
# apt list --upgradable
Upgrade to Debian Stretch

We have come to the most exciting part, which is the actual Jessie upgrade to Debian Stretch system. During the upgrade you may be asked:

There are services installed on your system which need to be restarted when certain libraries, such as libpam, libc, and libssl, are upgraded. Since these restarts may cause interruptions of service for the system, you will normally be prompted on each upgrade for the list of services you wish to restart. You can choose this option to avoid being prompted; instead, all necessary restarts will be done for you automatically so you can avoid being asked questions on each library upgrade.

Restart services during package upgrades without asking?
The choice is about whether you wish the system to restart your services automatically during the system upgrade or you wish to do it manually or after the system is fully upgrade to Stretch. When ready, execute the bellow commands to commence the Debian Stretch upgrade process:
# apt-get upgrade
# apt-get dist-upgrade
At this stage you should have your Jessie Debian Linux system fully upgraded to Debian Stretch. Follow, this guide to check your current Debian version. Once again check for obsolete packages so there are no surprises down the track:
# aptitude search '~o'
Congratulations to your fully upgraded Debian 9 Stretch Linux system.

&nbsp;

From:   https://linuxconfig.org/how-to-upgrade-debian-8-jessie-to-debian-9-stretch