---
title: 多线程gzip压缩神器---pigz
tags:
  - Linux
  - pigz
  - tools
url: archives/752.html
id: 752
categories:
  - Default Category
date: 2016-04-02 10:32:10
---

Fastq文件为纯文本文件，占用的硬盘空间较大，所以一般都会将Fastq文件压缩成gz格式，很多软件也支持fastq的gz格式输入。我用过python读取gzip，非常方便。单纯的通过gzip的命令压缩fastq，效率非常非常慢，据说是没有利用整个机器的cpu。

于是我就找到了pigz这款神器，可以在压缩数据时，发挥多核多处理器的优势，简而言之就是利用多线程进行gzip任务，比单纯的gzip压缩要快很多，有人测试快了5倍多（因为gzip压缩100G的文件时间是太长了，我也就没有测试）。

# pigz

官网  http://www.zlib.net/pigz/      

pigz, which stands for parallel implementation of gzip, is a fully functional replacement for gzip that exploits multiple processors and multiple cores to the hilt when compressing data.

# 安装pigz

```
wget http://zlib.net/pigz/pigz-2.3.3.tar.gz
tar -xvzf pigz-2.3.3.tar.gz
#如果提示不是gz格式，请尝试  tar -xvf pigz-2.3.3.tar.gz
cd pigz-2.3.3.tar.gz
make
如果报错 pigz.c:(.text.startup+0xca): undefined reference to `deflateEnd' gcc
请在第八行$(CC) $(LDFLAGS) -o pigz $^ -lpthread -lm 后面添加-lz选项，表示link libz
```




# 运行pigz

pigz -h 可以看到它的command option。

运行pigz和简单，和gzip的命令差不多，比如

<pre># -c 表示打印到标准输出std，如果没有-c选项，则会生成一个后缀为gz的压缩文件。
pigz -c file > file.gz
# -k 表示压缩后不删除源文件
pigz -k file</pre>  

<!--more-->

当然你可以继续优化命令，
--blocksize mmm 设置压缩块block的大小，默认为128kb
-0 to -9, -11设置压缩水平，值越大，压缩率越高，当然耗费的时间也就越长
等等

# 测试

压缩一个120G的文件，默认参数下，耗时25分钟

生成的gzip文件，可以通过gunzip解压缩

\#####################################################################
\#版权所有 转载请告知 版权归作者所有 如有侵权 一经发现 必将追究其法律责任
\#Author: Jason
\####################################################################