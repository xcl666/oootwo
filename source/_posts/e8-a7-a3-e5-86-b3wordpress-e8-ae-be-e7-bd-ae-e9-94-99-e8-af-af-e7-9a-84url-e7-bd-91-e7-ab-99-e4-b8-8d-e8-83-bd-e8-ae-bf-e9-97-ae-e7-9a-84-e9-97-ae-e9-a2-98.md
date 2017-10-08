---
title: 解决WordPress设置错误的url网站不能访问的问题
id: 5
categories:
  - LAMP
date: 2017-07-28 09:18:37
tags:
---

通过WordPress后台首选项更改了网站url地址之后，网站就会出现访问不了的情况，一般来说，网站后台也登陆不上去了，我从网上寻找到了四种方法，这四种方法前三种都是需要登陆到后台的，但实际上出错后，都不能登陆后台了，没法登陆后台进行调整！所以我用了第四种方法，通过修改数据库里面的内容修改成功！

**第一种、修改wp-config.php**

1、在wp-config.php中，添加以下两行内容：
define(‘WP_HOME’,’http://www.yourdomain.com’);
define(‘WP_SITEURL’,’http://www.yourdomain.com’);

www.yourdomain.com代表你的新地址

2、登录后台，在 “常规 -&gt; 设置”重新配置新博客地址（HOME）和安装地址（SITEURL），**成功后一定记得删除上面添加的内容。**

**第二种、修改functions.php**

functions.php指的是位于当前博客主题目录内，可以自定义一些主题函数。

1、在functions.php中，添加以下两行内容：

update_option(’siteurl’,’http://www.yourdomain.com’);
update_option(‘home’,’http://www.yourdomain.com’);

同样，www.yourdomain.com代表你的新地址

2、登录后台，在 “常规 -&gt; 设置”重新配置新博客地址（HOME）和安装地址（SITEURL），**成功后一定记得删除上面添加的内容。**

**第三种、修改wp-config.php（自动更新地址）**

1、在wp-config.php中，添加下面一行内容：
define(‘RELOCATE’,true);

2、登录后台地址，WP将自动更新安装地址（SITEURL），手动修改博客地址（HOME）地址即可，**成功后一定记得删除上面添加的内容。**

**第四种、修改数据库**

1，登录到你的管理页面，找到 **wp_options** 表

2，将表中的 **siteurl** 和 **home** 字段修改为当前的新域名

具体的sql为： UPDATE wp_options SET option_value=replace(option_value,'http://错误的url','http://正确的url') WHERE option_name='home' OR option_name='siteurl';如果不行，可以执行一下commit;注意sql中的字符格式和语句后面的分号。

这次问题修正，就是采用了这种方法，完美解决WordPress设置错误的域名后出现的访问问题。
<div> </div>
本文原地址：[http://qitiancom.com/archives/1099](http://qitiancom.com/archives/1099 "解决WordPress更改新域名后网站不能访问的问题")