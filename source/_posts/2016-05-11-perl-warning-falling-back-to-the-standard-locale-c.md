---
title: 'perl: warning: Falling back to the standard locale ("C")'
tags:
  - Perl
url: archives/757/index.html
id: 757
categories:
  - Default Category
date: 2016-05-11 18:02:47
---

出现该问题 Falling back to the standard locale ("C") 因为locales包没有安装或者没有配置。如果你在安装新的包时，出现该问题，先确定locales包是否安装。

apt-get install locales

该命令会安装locales包或者提示已经安装，如果提示已经安装，可以尝试重新配置locales

dpkg-reconfigure locales

解决好问题之后，重新运行需要安装的新包的命令。