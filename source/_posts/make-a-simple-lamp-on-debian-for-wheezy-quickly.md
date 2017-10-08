---
title: Make a simple LAMP on debian for Wheezy quickly
id: 43
categories:
  - LAMP
date: 2016-06-16 04:06:02
tags:
---

1, sudo apt-get install vsftpd

sudo vim /etc/vsftpd.conf

Uncomment the two sentences:

#local_enable=YES

#write_enalbe=YES

2, sudo apt-get install wordpress curl apache2 mysql-server

&nbsp;

1, vim /etc/apache2/sites-availablle/wp
Add this content:
Alias /wp/wp-content /var/lib/wordpress/wp.content
Alias /wp /usr/share/wordpress
&lt;Directory /usr/share/wordpress&gt;
Options FollowSymLinks
AllowOverride Limit Options FileInfo
DirectoryIndex index.php
Order allow,deny
Allow from all
&lt;/Directory&gt;
&lt;Directory /var/lib/wordpress/wp-content&gt;
Options FollowSymLinks
Order allow,deny
Allow from all
&lt;/Directory&gt;
2, Enalbe the site
# a2ensite wp
# service apache2 reload
3, vim /etc/wordpress/config-oootwo.com.php
Add this content:
&lt;?php
define('DB_NAME', 'wordpress');
define('DB_USER', 'wordpress');
define('DB_PASSWORD', 'password');
define('DB_HOST', 'localhost');
define('WP_CONTENT_DIR', '/var/lib/wordpress/wp-content');
?&gt;
!!! replace password with a suitably secure password
4, vim ~/wp.sql
Add this content:
CREATE DATABASE wordpress;
GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,ALTER
ON wordpress.*
TO wordpress@localhost
IDENTIFIED BY 'password';
FLUSH PRIVILEGES;
!!! replace password with a suitably secure password
# cat ~/wp.sql | mysql --defaults-extra-file=/etc/mysql/debian.cnf

5, Go to http://oootwo.com/wp to complete it.