---
title: 安装黑苹果
tags:
  - Mac
  - OX 
url: archives/1102/index.html
id: 1102
categories:
  - Default Category
date: 2020-05-29 16:55:23
---

最近电脑老是蓝屏，很是恼人，怀疑是win10系统的原因，重装了好几次还是蓝屏，于是决定装个黑苹果，用macOS系统（装好黑苹果MacOS 10.15 Catalina之后，发现可能是硬盘的问题导致蓝屏的，pity）。总结一下过程，看教程的时候很麻烦，实操一遍之后，回顾一下，其实还是蛮简单的，大致过程和装windows一样，就是多了添加clover引导，方便黑苹果从硬盘引导而不是U盘。下面是总结了一下过程，不是详细，方便以后再装

# 1，设置好分区

此电脑-管理-磁盘管理

（1）确保格式为GPT格式（GUID）

（2）确保有EFI分区

（3）压缩卷，给空出来的卷新建卷，不要选择格式化这个卷（安装黑苹果的过程中会进行）

（4）这个新建的卷就是安装黑苹果的分区

# 2，制作 MacOS 安装盘

## （1）下载镜像

强烈推荐 “黑果小兵“ 的网站： [https://blog.daliansky.net/](https://blog.daliansky.net/)

上面可以找OS的镜像，含有Clover引导

## （2）制作安装U盘

下载Transmac: [https://transmac.en.softonic.com/](https://transmac.en.softonic.com/)

有15天的试用期

选择 format with disk image，选择下载的OS文件，等待完成

# 3，安装Mac OS

## （1）设置BIOS

不同的电脑的BIOS稍微不同，我看多数涉及下面这两个，其他的还需要自己搜下

比如SATA Operation 勾选 AHCI

Secure Boot Enable 勾选 Disable

## （2）设置BIOS为UEFI U盘启动

通过U盘进入Clover引导之后，选择安装Install macOS ，中间会重启一次，重启之后，选择Install macOS Mojave from “你设置的盘”

等待系统安装好

# 4，设置Clover引导

## （1）复制Clover文件夹

下载Mac版本的Clover configurator [http://www.pc6.com/mac/294926.html](http://www.pc6.com/mac/294926.html)，不拔安装U盘的情况下，在挂载分区的选项中把系统的ESP和U盘的ESP分区挂载上。

复制U盘ESP分区中的clover文件到到系统的ESP分区EFI文件夹下（和mircosoft同级）

## （2）利用bootice添加Clover引导

在原来的windows系统下，或者通过Win PE，利用Disk Genius普通版即可，[https://www.diskgenius.cn/](https://www.diskgenius.cn/) ，把系统的ESP分配一个盘符

下载安装bootice之后，[https://bootice.en.softonic.com/](https://bootice.en.softonic.com/)

Bootice-UEFI0修改启动序列-添加，在路径上，选择ESP下EFI/CLOVER/CLOVERX64.efi，名称可以自己设置成Clover Boot Manager（开机的时候就是显示这个）

# 5，大功告成

开机的时候选择不同的引导进入不同的系统，这样也实现了单硬盘双系统。

参考：

[https://hackintosh.kirainmoe.com/an-zhuang-zhong/efi-ti-huan-jiao-cheng](https://hackintosh.kirainmoe.com/an-zhuang-zhong/efi-ti-huan-jiao-cheng)

[https://blog.daliansky.net/macOS-Catalina-10.15.5-19F96-Release-version-with-Clover-5118-original-image-Double-EFI-Version-UEFI-and-MBR.html](https://blog.daliansky.net/macOS-Catalina-10.15.5-19F96-Release-version-with-Clover-5118-original-image-Double-EFI-Version-UEFI-and-MBR.html)

[https://blog.csdn.net/qq_28735663/article/details/99695786](https://blog.csdn.net/qq_28735663/article/details/99695786)
