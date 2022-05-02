---
title: 误删hyper-v的avhdx文件
tags:
  - VM
url: archives/1061.html
id: 1061
categories:
  - Default Category
date: 2019-05-19 14:34:05
---
因为对hyper-v不是很熟悉，点了一下检查点，生成了一个avhdx文件，这个文件其实后续hyper-v会将其合并到vhdx的虚拟磁盘中。而我当时手贱手工的删除了avhdx文件，导致hyper-v找不到这个文件，vhdx也挂起等待合并，虚拟机迟迟不能启动。

有一种解决办法是文件恢复，但我用了几个文件都没有恢复成。实验室师兄（超级牛）新建了一个虚拟机挂载已有的vhdx文件，尝试用vhdx文件启动，显示不能启动，但在新的虚拟机下没有提示要合并，提示老系统的vhdx还有戏。

于是又新建了一个虚拟机实例，创建虚拟机实例之后，尝试将以前的vhdx文件挂载到新的虚拟机上，重启发现竟然以老的系统启动了。感谢能够启动，避免实验室的数据丢失。

![](/wp/f4w/2020/2019-05-19-hyper-v.png) 

根据结果反推，第一个shimx64.efi和Ubuntu.vhdx都是以前的系统，第二个shimx64.efi新的虚拟机的，硬盘驱动器已经换成了老系统的。

\#####################################################################
\#版权所有 转载请告知 版权归作者所有 如有侵权 一经发现 必将追究其法律责任
\#Author: Jason
\#####################################################################