---
title: Failed to mount 大容量的RAID组
tags:
  - Linux
  - Ubuntu
url: archives/1127/index.html
id: 1127
categories:
  - Default Category
date: 2020-08-31 01:22:23
---

我们的存储服务器有两组RAID，容量均大于150T，我在mount的时候，提示我

```
NTFS signature is missing.
Failed to mount '/dev/sdc': Invalid argument
The device '/dev/sdc' doesn't seem to have a valid NTFS.
Maybe the wrong device is used? Or the whole disk instead of a
partition (e.g. /dev/sda, not /dev/sda1)? Or the other way around?
```

是因为没有分区导致的，分区之后就可以了。分区的命令

```
# 使用parted命令进行分区,等同parted; select /dev/sdc
parted /dev/sdc 

# 创建分区表
mklabel gpt 

# 使用print命令查看当前分区情况
print 

# 留1M的空余空间，目的是为了让数据块整齐，提高磁盘的运行效率, -1表示分区的结尾  意思是划分整个硬盘空间为主分区
mkpart primary 1 -1 

p  # print的简写

# 使用q命令退出, 
quit 

# 退出之后会提示
会提示Information: You may need to update /etc/fstab.


# 格式化分区，为分区写入文件系统,格式为ext4
mkfs –t ext4 /dev/sdc1 # 格式化分区

# 使用blkid命令，找到 UUID，然后编辑 /etc/fstab，实现自动挂载
vim /etc/fstab

UUID=******	directory	ext4	defaults	0	0
```
# 参考:

https://www.cnblogs.com/kreo/p/9462641.html

https://www.cnblogs.com/saszhuqing/p/9964262.html



