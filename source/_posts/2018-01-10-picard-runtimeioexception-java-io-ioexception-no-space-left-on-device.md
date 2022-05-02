---
title: 'Picard---RuntimeIOException: java.io.IOException: No space left on device'
tags:
  - Picard
url: archives/798.html
id: 798
categories:
  - Default Category
date: 2018-01-10 20:13:11
---

在用Picard跑sortSam或者markDuplicate的时候，报错

**RuntimeIOException: java.io.IOException: No space left on device**

提示硬盘空间不足，实际上节点的硬盘空间是够的。这是因为Picard在做这两个处理的时候，会生成临时文件，临时文件默认储存在系统的tmp文件夹。这个文件夹内的文件存储一些程序和软件的临时文件，在RHEL6中，系统自动清理/tmp文件夹的默认时限是30天。可以通过/etc/cron.daily/tmpwatch配置,在Ubuntu中，系统自动清理/tmp文件夹的时限默认每次启动。而全基因组和全外显子组的数据非常大，现在分给系统的空间都很小，导致tmp文件夹写满而报错。

## **处理方法：**

在个人home文件夹下，新建一个tmp文件夹，每次运行picard的时候，指定IO临时文件夹为这个文件夹。

```
mkdir $HOME/tmp
java -Xmx2g -Djava.io.tmpdir=$HOME/tmp -jar SortSam.jar SORT_ORDER=coordinate INPUT=input.bam OUTPUT=output.sort TMP_DIR=$HOME/tmp
```


不能使用~，picard会在工作目录下创建'~'文件夹。

参考：

https://www.biostars.org/p/42613/

https://www.cnblogs.com/hnrainll/archive/2011/06/08/2074976.html

\#####################################################################
\#版权所有 转载请告知 版权归作者所有 如有侵权 一经发现 必将追究其法律责任
\#Author: Jason
\#####################################################################