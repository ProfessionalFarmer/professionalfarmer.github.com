---
title: 确定物理网口对应的名称以及配置静态IP
tags:
  - Linux
  - Ubuntu
url: archives/1125/index.html
id: 1125
categories:
  - Default Category
date: 2020-08-26 05:02:23
---

# 确定物理网口对应的名称

在一台ubuntu的机器上，有四个物理网口，我想知道每个网口对应的MAC地址。使用ip a可以看到网口的MAC地址和名称，比如列出了ens1f0, ens1f1, ens4f0, ens4f1。
原来的网卡interface都是eth开头，后来改成了enp, ens等。

Names incorporating Firmware/BIOS provided index numbers for on-board devices (example: eno1)
Names incorporating Firmware/BIOS provided PCI Express hotplug slot index numbers (example: ens1)
Names incorporating physical/geographical location of the connector of the hardware (example: enp2s0)
Names incorporating the interfaces's MAC address (example: enx78e7d1ea46da)
Classic, unpredictable kernel-native ethX naming (example: eth0)

那么如何确定机器上的ens1f0对应的哪个物理网口呢，可以用ethtool来实现，ethtool是用于查询及设置网卡参数的命令。用ethtool -p enos1f1，看哪个网口在闪灯，就能确定这个物理网口对应的名称。记得不要插网线。

```
ethtool -p|--identify DEVNAME   Show visible port identification (e.g. blinking)
```

如果没有一个网口亮灯，很可能是因为网口不支持，则可以尝试ethtool -t enosf1f1，大概在4秒之后，网口的灯会亮，这个时候就可以确定enos1f1对应的具体的物理网口了。
```
ethtool -t|--test DEVNAME       Execute adapter self test
```

很简单的一个命令，知道了就很简单，不知道就很难想到。

# 配置静态IP

```
/etc/netplan/00-installer-config.yaml

network:
  ethernets:
    enp0s3:  # 网卡名
      addresses: [192.168.1.3/24] # ip地址和子网掩码，24对应255.255.255.0
      gateway4: 192.168.1.1 # 网关
      nameservers:
        addresses: [4.2.2.2, 8.8.8.8] # DNS
  version: 2
```

配置好了之后，生效
```
sudo netplan apply
```

#####################################################################
#版权所有 转载请告知 版权归作者所有 如有侵权 一经发现 必将追究其法律责任
#Author: Jason
#####################################################################




