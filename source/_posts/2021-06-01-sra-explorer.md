---
title: 用SRA-Explorer辅助下载测序数据
tags:
  - SRA
  - FASTQ
url: archives/1269.html
id: 1269
categories:
  - Default Category
date: 2021-06-01 10:35:20
---



下载数据的时候，偶然碰到了SRA-Explorer，感觉挺好用的，地址：[https://sra-explorer.info/](https://sra-explorer.info/)

这个页面本身非常小，见[https://github.com/ewels/sra-explorer](https://github.com/ewels/sra-explorer)，利用的是SRA API。

检索好之后，选择你想下载的样本，点击Add ** to collection，然后点击右上角saved datasets，页面下方就可以原始的fastq的链接，用curl下载fastq的命令，用aspera下载fastq的命令，还有下载SRA的命令，以及样本的metadata。非常好用。

![](/wp/f4w/2021/2021-06-01-SRA-Explorer.png)

和SRA的Run Selector类似，[https://www.ncbi.nlm.nih.gov/Traces/study/?](https://www.ncbi.nlm.nih.gov/Traces/study/?)

#####################################################################
\#版权所有 转载请告知 版权归作者所有 如有侵权 一经发现 必将追究其法律责任
\#Author: Jason
#####################################################################

