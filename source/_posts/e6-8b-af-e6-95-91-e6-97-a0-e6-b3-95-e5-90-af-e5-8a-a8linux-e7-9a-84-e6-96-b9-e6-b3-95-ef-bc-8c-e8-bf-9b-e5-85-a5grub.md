---
title: 拯救无法启动linux的方法，进入grub
id: 92
categories:
  - Linux System
date: 2017-10-02 16:50:23
tags:
---

ls

set root=(hd0,gpt7)

set prefix=(hd0,gpt7)/boot/grub/

insmod normal

normal

仅仅是注册话就很简单了， efibootmgr 可以很方便地完成这个工作，

# efibootmgr -c -d /dev/nvme0n1 -p X -l \\EFI\\opensuse\\shim.efi -L opensuse-secure
其中，

-c 表示生成一个新的启动项；
-d /dev/nvme0n1 表示该启动项对应的文件在磁盘 /dev/nvme0n1 中，如果有多个磁盘，可能后面结尾的数字就不是 1；
-p X 表示启动项对应的文件在上述磁盘的第 X 个分区中；
-l \\EFI\\opensuse\\shim.efi 表示该启动项对应的启动文件，其中路径是相对于 ESP 分区的根目录（/）的，使用 \\ 这样的分隔符，如果不是 Secure Boot，则需要将上面的 shim.efi 改成 grubx64.efi；
-L opensuse-secure 表示新建启动项在EFI 内部启动管理器中的标签（名称）为 opensuse-secure。