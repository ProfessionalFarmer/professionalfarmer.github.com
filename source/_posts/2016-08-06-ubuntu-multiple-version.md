---
title: Ubuntu下安装java和多版本java共存控制
tags:
  - Java
url: archives/766.html
id: 766
categories:
  - Default Category
date: 2016-08-06 12:22:27
---

教你通过命令jdk7，jdk8就可以优雅的切换java版本

我在机器上已有java7（java1.7），目前而言java7应该是用的最广泛的，被java8取代还需要一段时间。不过我遇到最新版的picard要求java8版本，才遇到了安装新版java的问题，并且我不想删掉老版本java，我希望很方便的调用。

我查找的方法介绍，大部分都是通过update-alternatives --config java来选择，个人不喜欢这种方法。下面介绍一种比较优雅的方法，通过一个命令就能切换java版本。

# 下载jdk

下载页面  [http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)

选在对应的版本，如果版本不对应，在运行java时会报 **no such file or directory**。

一般放在  /usr/jvm/jdk   /opt/Java/jdk/   /usr/lib/jvm _等目录下，当然也可以放在其他地方。

**解压缩下载后的文件**

# 优雅的控制java版本

**编辑~/.profile或者~/.bashrc**

## 设置两个版本的路径

```
export JAVA7_HOME='/path/to/jdk1.7.**'
export JAVA8_HOME='/path/to/jdk1.8.***'
```


## 设置默认java版本

```
export JAVA_HOME=$JAVA7_HOME
export JRE_HOME=$JAVA_HOME/jre
export CLASSPATH=.:$JAVA_HOME/lib:$JRE_HOME/lib:$CLASSPATH
export PATH=$JAVA_HOME/bin:$JRE_HOME/bin:$PATH
```


## 转换版本命令

```
alias jdk8='export JAVA_HOME=$JAVA8_HOME && export JRE_HOME=$JAVA_HOME/jre && export CLASSPATH=.:$JAVA_HOME/lib:$JRE_HOME/lib:$CLASSPATH && export PATH=$JAVA_HOME/bin:$JRE_HOME/bin:$PATH'
alias jdk7='export JAVA_HOME=$JAVA7_HOME && export JRE_HOME=$JAVA_HOME/jre && export CLASSPATH=.:$JAVA_HOME/lib:$JRE_HOME/lib:$CLASSPATH && export PATH=$JAVA_HOME/bin:$JRE_HOME/bin:$PATH'
```


还有一步 source ~/.profile或者source ~/.bashrc

这样就可以通过jdk7命令切换到java7版本，通过jdk8命令切换到java8版本。默认是java7版本。这样可以避免通过 update-java-alternatives 命令来配置和控制java版本了。

# 参考

[http://stackoverflow.com/questions/26252591/mac-os-x-and-multiple-java-versions](http://stackoverflow.com/questions/26252591/mac-os-x-and-multiple-java-versions)

[http://jingyan.baidu.com/article/647f0115bb26817f2048a871.html](http://jingyan.baidu.com/article/647f0115bb26817f2048a871.html)

\#####################################################################
\#版权所有 转载请告知 版权归作者所有 如有侵权 一经发现 必将追究其法律责任
\#Author: Jason
\####################################################################