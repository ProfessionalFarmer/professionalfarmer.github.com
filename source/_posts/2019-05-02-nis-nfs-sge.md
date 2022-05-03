---
title: NIS+NFS+SGE
tags:
  - Cluster
  - NFS
  - NIS
  - SGE
url: archives/1057/index.html
id: 1057
categories:
  - Default Category
date: 2019-05-02 20:48:43
---

需求，把多台服务器组成一个cluster(**SGE**)，把一台电脑（比如存储）的home文件件共享给其他服务器(**NFS**)，共用一个home文件夹，并进行用户的统一管理(**NIS**)。

操作系统为操作系统：CentOS，用virtual box虚拟出来的系统做测试。
server端：10.0.2.5
client或compute端：在同样网段

![](/wp/f4w/2020
/2019-05-02-NSF-SGE-NIS.png)

# 1，NFS共享存储

通过nfs，实现每台服务器都有同样的路径和文件，便于后续集群管理。这里共享两个路径，一个是server端的/home路径，实现每个服务器都有同样的家目录，一个是/opt/gridengine用于安装SGE。

## 1.1 Server端：

安装相关软件，NFS的端口是不固定的（因此如果客户端连不上的时候，往往需要iptables -F清理一下），客户端要准确的获得NFS服务器所使用的端口，就需要RPC服务。RPC最主要的功能就是记录每个NFS功能所对应的端口号，并且在NFS客户端请求时将该端口和功能对应的信息传递给请求数据的NFS客户端，让客户端可以链接到正确的端口上去，从而实现数据传输。
```
yum install nfs-utils rpcbind
```

### 开机启动rpcbind

```
systemctl enable rpcbind.service
```

### 开启rpcbind

```
systemctl start rpcbind.service
```

### 设置要共享的目录

```
mkdir /opt/gridengine
vi /etc/exports
/home 10.0.2.0/255.255.255.0(rw,sync)
/opt/gridengine 10.0.2.0/255.255.255.0(rw,sync)
```

### nfs开机启动和开启服务

```
systemctl enable nfs
systemctl start nfs
```

### 生效export

```
exportfs -r -v
```

## 1.2 客户端：

```
yum install nfs-utils rpcbind
systemctl enable  rpcbind.service
systemctl restart rpcbind.service
systemctl enable nfs
systemctl start  nfs
```

### 设置自动挂载，用tab分割，不是空格

```
mkdir /opt/gridengine
vi /etc/fstab
10.0.2.5:/home	/home	nfs	defaults	0	0
10.0.2.5:/opt/gridengine	/opt/gridengine	nfs	defaults	0	0
```

### 挂载

```
mount -a
```

这样的话，客户端服务器的home目录都是server端的home家目录。

# 2，NIS(Network Information Service)

通过NIS实现帐号的统一权限管理和认证，避免在多台服务器上重复开设帐号

## 2.1 Server端：

 <!--more-->

### 安装相关库

```
yum -y install ypserv,ypbind,yp-tools,rpcbind
```

### 配置NIS domain，增加NISDOMAIN和启用的端口

```
vi /etc/sysconfig/network
NISDOMAIN=yourdomain
YPSERV_ARGS="-p 1011"
```

### 增加开机自动加入NIS域

```
vi /etc/rc.d/rc.local
/bin/nisdomainname yourdomain
```

### 设置NIS服务器访问权限

编辑NIS配置文件，允许特定的主机访问NIS服务器，可以是特定ip，也可以是特定网段，比如下面是2段的

```
vi /etc/ypserv.conf
10.0.2.0/255.255.255.0 : * : * : none
```

### 让yppasswdd启动在固定端口，方便防火墙管理

```
vi /etc/sysconfig/yppasswdd
YPPASSWDD_ARGS="--port 1012"
```

### 设置开机启动和启动服务，先启动rpcbind再启动ypserv

```
systemctl enable rpcbind  
systemctl enable ypserv  
systemctl enable yppasswdd.service
systemctl start rpcbind  
systemctl start ypserv
```

### 建立数据库，将nis服务器端的用户信息导入，当用户信息更新时，也需重新执行该命令更新数据库

```
/usr/lib64/yp/ypinit -m
```

### 在server 端新增账号或者删除账号或者修改账号信息后，更新NIS账户和资料库

```
make -C /var/yp
make -C /var/yp passwd
```

## 2.2 客户端

### 安装NIS相关库

```
yum -y install ypbind yp-tools
```

### 在网络项加入NIS域

```
vi /etc/sysconfig/network
NISDOMAIN=yourdomain
YPSERV_ARGS="-p 1011"
```

### 开机自动加入NIS域

```
vi /etc/rc.d/rc.local
/bin/nisdomainname yourdomain
```

### 修改用户密码的认证顺序文件,用于管理系统中多个配置文件查找的顺序

```
vi /etc/nsswitch.conf 
...
passwd:    files nis sss
shadow:    files nis sss
group:     files nis sss
...
hosts:      files nis dns
...
```

### 修改客户端配置文件,输入NIS服务器信息

```
vi /etc/yp.conf
domain yourdomain server 10.0.2.5
```

### 修改系统认证文件，启用nis

```
vi /etc/sysconfig/authconfig
USENIS=yes
```

### 设置PAM授权，添加nis

```
vi /etc/pam.d/system-auth
password sufficient pam_unix.so sha512 shadow nis nullok try_first_pass use_authtok
```

### 开机启动和启用服务

```
systemctl enable ypbind
systemctl enable rpcbind
systemctl start ypbind
systemctl start rpcbind
```

ypbind启动不起来的时候，用systemctl status ypbind发现nis server 没反应
server和client端用iptables -F清理一下

此时，可以在client端su切换成server端的其他账号，而本地并没有创建这个帐号

# 3, SGE Cluster

组成集群，便于分布式计算和任务调度。这个sge是son grid engine，在oracle关闭grid engine项目之后的继续维护项目，但现在也好久没更新了。

SGE安装包下载地址：
https://arc.liv.ac.uk/trac/SGE

https://arc.liv.ac.uk/downloads/SGE/releases/

## 3.1 server端：主控节点，qmaster节点

### 修改hostname

```
hostnamectl set-hostname qmaster.local
```

### 修改hosts文件，添加主控节点和两个计算节点信息

```
vi /etc/hosts
10.0.2.5 qmaster.local qmaster
10.0.2.7 compute01.local compute01
10.0.2.8 compute02.local compute02
```

### 设置SGE_ROOT环境变量,并生效

```
vi /etc/profile
/etc/profile
export SGE_ROOT=/opt/gridengine
export PATH="${SGE_ROOT}/bin/lx-amd64:$PATH"

source /etc/profile
```

### 命令行执行，安装相关库

```
yum -y install epel-release
yum -y install jemalloc-devel openssl-devel ncurses-devel pam-devel libXmu-devel hwloc-devel hwloc hwloc-libs java-devel javacc ant-junit libdb-devel motif-devel csh ksh xterm db4-utils perl-XML-Simple perl-Env xorg-x11-fonts-ISO8859-1-100dpi xorg-x11-fonts-ISO8859-1-75dpi
```

### 添加sgeadmin用户组，及sgeadmin用户

```
groupadd -g 490 sgeadmin
useradd -u 495 -g 490 -m -d /home/sgeadmin -s /bin/bash -c "SGE Admin" sgeadmin
```

### 修改sudo文件，添加一行配置添加sgeadmin用户

```
visudo
%sgeadmin ALL=(ALL) NOPASSWD: ALL
```

### 下载并编译SGE，no java避免java带来的错误

```
wget https://arc.liv.ac.uk/downloads/SGE/releases/8.1.9/sge-8.1.9.tar.gz
tar -zxvf sge-8.1.9.tar.gz
cd sge-8.1.9/source/
sh scripts/bootstrap.sh -no-java -no-jni && ./aimk -no-java -no-jni 
export SGE_ROOT=/opt/gridengine && mkdir $SGE_ROOT
echo Y ' ./scripts/distinst -local -allall -libs -noexit
chown -R sgeadmin.sgeadmin /opt/gridengine
```

### 安装SGE qmaster节点

```
cd $SGE_ROOT
./install_qmaster
```

## 3.2计算节点

### 安装相关库

```
yum -y install hwloc-devel
```

### 修改hostname

```
hostnamectl set-hostname compute01.local
```

### 修改hosts文件，添加主控节点和两个计算节点信息

```
vi /etc/hosts
10.0.2.5 qmaster.local qmaster
10.0.2.7 compute01.local compute01
10.0.2.8 compute02.local compute02
```
或者scp把qmaster上hosts复制/etc/

### 添加sgeadmin用户组，添加sgeadmin用户

```
groupadd -g 490 sgeadmin
useradd -u 495 -g 490 -r -s /bin/bash -c "SGE Admin" sgeadmin
```

### 设置SGE_ROOT环境变量,并生效

```
vi /etc/profile
/etc/profile
export SGE_ROOT=/opt/gridengine
export PATH="${SGE_ROOT}/bin/lx-amd64:$PATH"

source /etc/profile
```

### 安装计算节点

```
cd $SGE_ROOT
./install_execd
cp /opt/gridengine/default/common/settings.sh /etc/profile.d/
source /etc/profile.d/settings.sh
```

如果报neither submit or admin host，则在qmaster上将这台电脑加为admin host或者submit host
qconf -ah compute01

### 启动计算节点

```
$SGE_ROOT/default/common/sgeexecd
```

这样的话，在qmaster用qhost就能看到每个计算节点的资源了，用qsub命令可以提交相关任务，有SGE负责管理计算资源。

参考：https://github.com/wangkaisine/SGE-On-CentOS
http://www.178pt.com/32.html

https://blog.csdn.net/younger_china/article/details/53130780
http://blog.sina.com.cn/s/blog_64aac6750101gwst.html

![](/wp/f4w/2020
/2019-05-02-NSF-SGE-NIS.png)
\##################################################################\###
\#版权所有 转载请告知 版权归作者所有 如有侵权 一经发现 必将追究其法律责任
\#Author: Jason
\#####################################################################