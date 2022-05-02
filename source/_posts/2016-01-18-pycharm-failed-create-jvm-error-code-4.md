---
title: PyCharm启动时报failed to create jvm error code 4
tags:
  - JVM
url: archives/731.html
id: 731
categories:
  - Default Category
date: 2016-01-18 22:23:33
---

pycharm failed to create JVM with error code 4 when launching pycharm.

![pycharm failed to create jvm](/wp/f4w/2020/2016-01-18-failed-to-create-jvm2.png)

In a ordinary way, you can decrease -Xmx and -XX option value in $IDE_HOMEBINidea.exe.vmoptions.

Another way, when pycharm invoking JVM, pycharm depends on its own vm options in VM optioins configuraion file.

![pycharm fail to create jvm](/wp/f4w/2020/2016-01-18-failed-to-create-jvm.png)

VM options can be set in JetBrainsPyCharm Community Edition 3.4.1bin. In the direcotry, there is a file named by pycharm.exe.vmoptions. You can decrease the -XX and -Xmx value in this file. Recommend 100M per time to decrease and try to open pycharm.