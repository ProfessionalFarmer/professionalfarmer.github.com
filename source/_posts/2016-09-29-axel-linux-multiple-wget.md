---
title: Axel - Linux下多线程下载工具
tags:
  - Linux
  - tool
url: archives/785/index.html
id: 785
categories:
  - Default Category
date: 2016-09-29 12:02:13
---

在linux环境下，用wget下载大文件，实在是件痛苦的事情，下载速度慢。这非常的不科学，于是找到了axel这个工具，可以实现在linux下多线程下载。并且可以实现断点续传。 Axel项目网站 https://wilmer.gaa.st/main.php/axel.html

安装
==

```bash
wget -c https://wilmer.gaa.st/downloads/axel-1.0b.tar.gz
tar zxvf axel-1.0b.tar.gz
cd axel-1.0b/
./configure
make
make instal
```

或者
==

apt-get install axel 参数 -n 指定线程数 -o 指定另存为目录 -s 指定每秒的最大比特数 -q 静默模式

测试
==

比如从UCSC上下载 938M 的参考基因组序列gz格式文件

axel -n 8 http://hgdownload.cse.ucsc.edu/goldenPath/hg38/bigZips/hg38.fa.gz

Initializing download: http://hgdownload.cse.ucsc.edu/goldenPath/hg38/bigZips/hg38.fa.gz
File size: 983659424 bytes
Opening output file hg38.fa.gz
Starting download

\[  0%\]  .......... .......... ..........  \[  41.3KB/s\]
\[  0%\]  .......... .......... ..........  \[ 179.5KB/s\]
\[  0%\]  .......... .......... ..........  \[ 423.4KB/s\]
\[  0%\]  .......... .......... ..........  \[ 583.9KB/s\]
\[  0%\]  .......... .......... ..........  \[ 772.0KB/s\]
\[  0%\]  .......... .......... ..........  \[ 801.8KB/s\]
\[  0%\]  .......... .......... ..........  \[ 802.1KB/s\]
\[  0%\]  .......... .......... ..........  \[ 813.1KB/s\]
\[  1%\]  .......... .......... ..........  \[ 843.5KB/s\]
\[ 99%\]  .......... .......... ..........  \[ 666.7KB/s\]
\[ 99%\]  .......... ......
Connection 7 finished
        ,,,,,,,,,, ,,,,,,,,,, ,,,,,,....  \[ 666.6KB/s\]
\[ 99%\]  .......... .......... ..........  \[ 666.7KB/s\]
\[ 99%\]  .......... .......
Connection 2 finished
        ,,,,,,,,,, ,,,,,,,,,, ,,,,,,,...  \[ 666.5KB/s\]
\[ 99%\]  .......... .......... ..........  \[ 663.1KB/s\]
\[ 99%\]  .......... .......... ..........  \[ 662.8KB/s\]
\[100%\]  ....
Connection 0 finished

Downloaded 938.1 megabytes in 24:09 seconds. (662.81 KB/s)