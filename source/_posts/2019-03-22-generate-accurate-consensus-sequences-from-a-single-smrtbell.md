---
title: Generate Accurate Consensus Sequences from a Single SMRTbell
tags:
  - Pacbio
url: archives/1044.html
id: 1044
categories:
  - Default Category
date: 2019-03-22 18:23:09
---

![Circular-Consensus-Sequence](/wp/f4w/2020/2019-03-22-PACBIO-ZMW-read.png)

bax2bam
=======

bax2bam -o mynewbam mydata.1.bax.h5 mydata.2.bax.h5 mydata.3.bax.h5

circus consensus sequence
=========================

![Circular-Consensus-Sequence](/wp/f4w/2020/2019-03-22-PB-PACBIO-Circular-Consensus-Sequence.png)

ccs –minLength=100 myData.subreads.bam myResult.bam

进行CCS由pacbio测序系统决定的，插入序列测多遍之后，可以用来校正随机错误。

参考
==

[https://github.com/PacificBiosciences/unanimity/blob/develop/doc/PBCCS.md](https://github.com/PacificBiosciences/unanimity/blob/develop/doc/PBCCS.md)