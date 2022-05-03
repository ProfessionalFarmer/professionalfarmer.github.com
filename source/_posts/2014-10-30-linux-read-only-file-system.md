---
title: Linux read only file system
tags:
  - Linux
url: archives/706/index.html
id: 706
categories:
  - Default Category
date: 2014-10-30 20:31:10
---

正用着的服务器在打开Netbean的时候报磁盘空间不足。

因为这台机器一直是自己在用，于是登陆root用户，du -sh /home/* 想看看最近有没有人其他人在这台机器上用导致磁盘空间不足。发现确实有人在用，于是想清理一下文件释放点空间。

但是这个时候报错 read only file system ！！ 我觉得，可能是由于硬盘满了，系统不再允许往里写的问题，还有一种可能是文件系统确实坏了，需要fsck。

在网上查了查解决办法，比如

`mount -o remount,rw / `

比如

`cat /ect/fatab`

比如

`fsck`

等等，但是要么不行，要么没有问题，在万念俱灰的时候，重启了下机器，竟然可以删除了，谢天谢地。

但是在删到一半的时候报错 kernel: journal commit I/O error (顿时心都碎了，前面还没弄好呢，又蹦出这个问题) 。fsck修复两个，但是依然报错 read only file system。再重启，在启动过程中，系统提示输入root密码fsck repaire修复。之后

 `fsck -y /`

问题是解决了，但还是没搞定什么原因造成的。另外如果想先备份出文件，建议先scp。