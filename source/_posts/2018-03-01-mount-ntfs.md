---
title: '解决 mount: unknown filesystem type ntfs'
tags:
  - Linux
  - Mount
url: archives/860/index.html
id: 860
categories:
  - Default Category
date: 2018-03-01 11:14:06
---


移动硬盘是ntfs格式的，服务器不能mount，报错 mount: unknown filesystem type 'ntfs'

解决方法：安装 NTFS-3G，官网 https://www.tuxera.com/community/open-source-ntfs-3g

安装

```
wget -c https://tuxera.com/opensource/ntfs-3g_ntfsprogs-2017.3.23.tgz
tar -xvzf ntfs-3g_ntfsprogs-2017.3.23.tgz 
cd ntfs-3g_ntfsprogs-2017.3.23
./configure 
make 
sudo make install
```




挂载

```
mount -t ntfs-3g /dev/sd**  /target
```



\#####################################################################
\#版权所有 转载请告知 版权归作者所有 如有侵权 一经发现 必将追究其法律责任
\#Author: Jason
\###########################################################################