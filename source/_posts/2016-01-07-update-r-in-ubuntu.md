---
title: ubuntu下升级更新R版本
tags:
  - R
url: archives/719/index.html
id: 719
categories:
  - Default Category
date: 2016-01-07 22:56:16
---

虽说用最早知道R是在大学的时候，那个时候因为生物信息的人都会R。实际上，我倒现在都不会R，一直在用JAVA，现在也转到python上了。感觉做转录组的牛人用R比较多。我也在计划学下R，毕竟很多统计和作图的包都是R包。

废话不多说了，为什么我不会R，却还要发这个帖子呢，因为我在做Fastq文件质控的时候，需要一个R包，我不会写R，但是会照猫画虎的用哈，不过在安装这个包的时候提示我`package not available for R`。当时想，是不是服务器上的版本有点老啊。于是弱弱的用百度搜了下，竟然有人说要先卸载再安装。我想，这不科学啊，还是谷歌了一下。

上干货

1，这一步的目的是添加cran到apt的源中，cran也可以换成其他的。

    sudo echo "deb http://mirrors.aliyun.com/CRAN/bin/linux/ubuntu/ trusty/" >> /etc/apt/sources.list

2，从公钥服务器上获得缺失的公钥，公钥服务器也可以换成其他地方的。Fetch the secure APT key

    gpg --keyserver keyserver.ubuntu.com --recv-key E084DAB9
    或者
    gpg --hkp://keyserver keyserver.ubuntu.com:80 --recv-key E084DAB9

4，导入公钥 Feed it to apt-key

    gpg -a --export E084DAB9 ' sudo apt-key add -

5， 

    sudo apt-get update && sudo apt-get install r-base

然后完成R语言的更新。<!--more-->

关注怎么更新R版本的童鞋们可以先退了。

其实，后来我升级完R后，还是出现package not available for R的问题，说明和R版本无关。没关系，我接着找原因，这篇[文（dian）章（wo）](http://altons.github.io/r/2013/06/23/when-package-xyz-is-not-available-for-a-specific-version-of-r/ "文（dian）章（wo）")。提出出现package not available for R的原因有两种，一种是cran镜像out of date，另外一种是没有特定R版本的二进制包。我不生产水，我是大自然的搬运工--内容粘贴如下：

> **When package XYZ is not available for a specific version of R**
> 
> When you try to install a package in R and you get the following message:
> 
> Warning in install.packages :
> package XYZ is not available (for R version x.xx.x)
> is normally down to:
> 
> *   CRAN mirror is out-of-date in which case you can change the repo by using:
> `install.packages("XYZ",repos = "http://cran.us.r-project.org/")`
> *   Package author have not created a binary package for the specific version of R.
> If the latter, here they are a set of simple steps to compile an R package from source.
> 
> 1.  Go to package's site, e.g. ggplot2
> 2.  Download the package source for your OS. For MacOS would be ggplot2_0.9.3.1.tgz
> 3.  Open an R session and type & run the following command:
> `install.packages("/path/to/file/packageName.tgz",repos = NULL, type="source")`
> and Voila! your package is now available for your version of R.
> Note: If package has dependencies you may try to install them using the standard install.packages() and if they are not available then do the above steps.

Ref：Thanks the authors

[http://stackoverflow.com/questions/10476713/how-to-upgrade-r-in-ubuntu](http://stackoverflow.com/questions/10476713/how-to-upgrade-r-in-ubuntu "http://stackoverflow.com/questions/10476713/how-to-upgrade-r-in-ubuntu")
