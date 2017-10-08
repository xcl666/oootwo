---
title: WordPress安装主题和插件显示“无法创建目录”解决方法
id: 13
categories:
  - LAMP
date: 2017-07-28 10:29:27
tags:
---

安装主题需要使用ftp进行上传，所以首先需要检查服务器是否安装了ftp。如果没有安装，需要先安装ftp。这里使用vsftpd举例，ftp用户直接使用root。

1、安装vsftpd：
<div id="crayon-597afdb9c3169437302713" class="crayon-syntax crayon-theme-henry crayon-font-sourcecodepro crayon-os-pc print-yes notranslate crayon-wrapped">
<div class="crayon-plain-wrap"></div>
<div class="crayon-main">
<table class="crayon-table">
<tbody>
<tr class="crayon-row">
<td class="crayon-nums ">
<div class="crayon-nums-content">
<div class="crayon-num">1</div>
</div></td>
<td class="crayon-code">
<div class="crayon-pre">
<div id="crayon-597afdb9c3169437302713-1" class="crayon-line"><span class="crayon-o">~</span><span class="crayon-p"># apt-get install vsftpd</span></div>
</div></td>
</tr>
</tbody>
</table>
</div>
</div>
启用root的使用权限
<div id="crayon-597afdb9c3179745397669" class="crayon-syntax crayon-theme-henry crayon-font-sourcecodepro crayon-os-pc print-yes notranslate crayon-wrapped">
<div class="crayon-plain-wrap"></div>
<div class="crayon-main">
<table class="crayon-table">
<tbody>
<tr class="crayon-row">
<td class="crayon-nums ">
<div class="crayon-nums-content">
<div class="crayon-num">1</div>
</div></td>
<td class="crayon-code">
<div class="crayon-pre">
<div id="crayon-597afdb9c3179745397669-1" class="crayon-line"><span class="crayon-o">~</span><span class="crayon-p"># vi /etc/ftpuser</span></div>
</div></td>
</tr>
</tbody>
</table>
</div>
</div>
将这个文件内的root删除

设置ftp为可写入状态
<div id="crayon-597afdb9c3180631457997" class="crayon-syntax crayon-theme-henry crayon-font-sourcecodepro crayon-os-pc print-yes notranslate crayon-wrapped">
<div class="crayon-plain-wrap"></div>
<div class="crayon-main">
<table class="crayon-table">
<tbody>
<tr class="crayon-row">
<td class="crayon-nums ">
<div class="crayon-nums-content">
<div class="crayon-num">1</div>
</div></td>
<td class="crayon-code">
<div class="crayon-pre">
<div id="crayon-597afdb9c3180631457997-1" class="crayon-line"><span class="crayon-o">~</span><span class="crayon-p"># vi /etc/vsftpd.conf</span></div>
</div></td>
</tr>
</tbody>
</table>
</div>
</div>
将其中的write_enable=YES，保存重启vsftpd服务
<div id="crayon-597afdb9c3186216439830" class="crayon-syntax crayon-theme-henry crayon-font-sourcecodepro crayon-os-pc print-yes notranslate crayon-wrapped">
<div class="crayon-plain-wrap"></div>
<div class="crayon-main">
<table class="crayon-table">
<tbody>
<tr class="crayon-row">
<td class="crayon-nums ">
<div class="crayon-nums-content">
<div class="crayon-num">1</div>
</div></td>
<td class="crayon-code">
<div class="crayon-pre">
<div id="crayon-597afdb9c3186216439830-1" class="crayon-line"><span class="crayon-o">~</span><span class="crayon-p"># service vsftpd restart</span></div>
</div></td>
</tr>
</tbody>
</table>
</div>
</div>
2、设置WordPress目录为可写

进入WordPress网站所在目录，修改themes/plugins两个文件夹权限
<div id="crayon-597afdb9c318d172317187" class="crayon-syntax crayon-theme-henry crayon-font-sourcecodepro crayon-os-pc print-yes notranslate crayon-wrapped">
<div class="crayon-plain-wrap"></div>
<div class="crayon-main">
<table class="crayon-table">
<tbody>
<tr class="crayon-row">
<td class="crayon-nums ">
<div class="crayon-nums-content">
<div class="crayon-num">1</div>
<div class="crayon-num">2</div>
</div></td>
<td class="crayon-code">
<div class="crayon-pre">
<div id="crayon-597afdb9c318d172317187-1" class="crayon-line"><span class="crayon-o">~</span><span class="crayon-p"># chmod 755 wp-content/themes</span></div>
<div id="crayon-597afdb9c318d172317187-2" class="crayon-line"><span class="crayon-o">~</span><span class="crayon-p"># chmod 755 wp-content/plugins</span></div>
</div></td>
</tr>
</tbody>
</table>
</div>
</div>
重启服务器，此时已经可以正常上传目录和主题
<div id="crayon-597afdb9c3193885652307" class="crayon-syntax crayon-theme-henry crayon-font-sourcecodepro crayon-os-pc print-yes notranslate crayon-wrapped">
<div class="crayon-plain-wrap"></div>
<div class="crayon-main">
<table class="crayon-table">
<tbody>
<tr class="crayon-row">
<td class="crayon-nums ">
<div class="crayon-nums-content">
<div class="crayon-num">1</div>
</div></td>
<td class="crayon-code">
<div class="crayon-pre">
<div id="crayon-597afdb9c3193885652307-1" class="crayon-line"><span class="crayon-o">~</span><span class="crayon-p"># service apache2 restart</span></div>
</div></td>
</tr>
</tbody>
</table>
原文地址：http://blog.zivers.com/post/240.html

</div>
</div>