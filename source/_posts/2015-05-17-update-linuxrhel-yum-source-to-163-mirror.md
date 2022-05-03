---
title: Update LinuxRHEL yum source to 163 mirror--更新yum源为163的镜像
tags:
  - Linux
  - yum
url: archives/713/index.html
id: 713
categories:
  - Default Category
date: 2015-05-17 20:47:44
---

open source mirror of 163:  [http://mirrors.163.com/](http://mirrors.163.com/ "http://mirrors.163.com/")

as a root user

<pre>cd /ect/yum.repos.d 
wget http://mirrors.163.com/.help/CentOS5-Base-163.repo
yum clean all
yum makecache</pre>

But an error occurs:

<pre>> Timeout on [http://mirrors.163.com/centos/6Server/os/x86_64/repodata/repomd.xml](http://mirrors.163.com/centos/6Server/os/x86_64/repodata/repomd.xml "http://mirrors.163.com/centos/6Server/os/x86_64/repodata/repomd.xml")
> PYCURL ERROR 22- The requested URL returned errer: 404</pre>

I can't find this directory in 163's webserver (but I do find [http://mirrors.163.com/centos/6/os/x86_64/repodata/repomd.xml](http://mirrors.163.com/centos/6/os/x86_64/repodata/repomd.xml "http://mirrors.163.com/centos/6/os/x86_64/repodata/repomd.xml")), so I guess some thing wrong in .repo file.

As for me, I changed all 

`baseurl=http://mirrors.163.com/centos/$releasever`

to

`baseurl=http://mirrors.163.com/centos/6`

To here, your problem might be solved. For my question about repomd.xml directory is solved, but error of "Timeout on ***" and "cannot retrieve repository metadata" still occur.

I looked up /etc/yum.conf file, and found "proxy" field is available (this may lead me unable to connect 163's webserver). So I comment them out and yum command works out.