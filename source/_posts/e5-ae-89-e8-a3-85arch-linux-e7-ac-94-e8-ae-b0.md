---
title: 安装Arch Linux笔记
id: 9
categories:
  - Linux System
date: 2016-05-26 17:54:22
tags:
---

1，dos硬盘安装
一，easybsd安装，grub4dos，添加命令
title Install ArchLinux
root (hd0,0)
kernel /vmlinuz archisolabel=archlinux
initrd /archiso.img
boot
二，遇到shell
mkdir /tmpmnt
mount -r -t ntfs /dev/sda1 /tmpmnt
modprobe loop
losetup /dev/loop6 /tmpmnt/archlinux.iso
ln -s /dev/loop6 /dev/disk/by-label/archlinux
exit
然后正常安装
2，uefi，gpt硬盘安装（未成功）（无法安装grub，下次尝试，借鉴winly-efi）
使用的是usb安装，使用USBWriter1.3刻录U盘安装
提到具体的硬盘分区问题
cfdisk
第一个分区2M，bios_grub
parted set 1 bios_grub on
第二个分区1G，efi system
parted set 2 boot on
注意安装dosfstools
pacman -S dosfstools
mkfs.fat -F32 /dev/sda2
第三个分区/ 10G
3,开始安装
参考http://www.cnblogs.com/mad/p/3280041.html
图文讲解比较容易理解
分区
cfdisk
格式化
mkfs.ext4 /dev/sda1
挂载分区
mount /dev/sda1 /mnt
选择镜像点
vim /etc/pacman.d/mirrorlist
把163的复制到第一行
安装基本系统
pacstrap -i /mnt base
生成fstab
genfstab -U -p /mnt &gt;&gt; /mnt/etc/fstab
配置系统
vi /etc/locale.gen
添加
en_US.UTF-8 UTF-8
执行
locale-gen
echo LANG=en_US.UTF-8 &gt; /etc/locale.conf
export LANG=en_US.UTF-8
起名
echo myhostname &gt; /etc/hostname
配置网络
systemctl enable dhcpd.service
设置密码
passwd
4,安装grub 这个非常重要
一，dos硬盘，传统legacy启动方式，安装上面的来直接可以
pacman -S grub
grub-install --target=i386-pc --recheck /dev/sda
grub-mkconfig -o /boot/grub/grub.cfg
二，gpt硬盘，UEFI启动方式，按照下面的来安装（--boot-directory=/boot/EFI ）
mkdir /mnt/boot/EFI
mount /dev/sda2 /mnt/boot/EFI
grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=grub --recheck
grub-mkconfig -o /boot/grub/grub.cfg
卸载mnt，重启
exit
umount /mnt
shutdown -r now
5,安装桌面环境
pacman -S xorg-server xorg-server-utils xorg-xinit
先看
lspci | grep VGA
pacman -Ss xf86-video | less
pacman -S xf86-video-nv
笔记本触摸板驱动
pacman -S xf86-input-synaptics
测试X环境
pacman -S xorg-twm xorg-xclock xterm
startx
exit
pkill X
安装xfce4
pacman -S lxdm xfce4
startxfce4
安装字体
pacman -S wqy-microhei wqy-zenhei wqy-bitmapfont
添加一个用户
pacman -S sudo
useradd -m yourname
passwd yourname
然后把该用户添加到一些组：　audio disk locate network optical power storage video wheel systemd-journal
gpassd -a yourname wheel
6,设置xfce4自启动
重启
echo "exec startxfce4" &gt;&gt; /home/user/.xinitrc
systemctl enable lxdm.service
注意：
文中提到工具都可以在ftp://oootwo.com中下载。