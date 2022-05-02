---
title: SAM文件中的soft clipping和hard clipping
tags:
  - clip alignment
  - SAM
url: archives/726.html
id: 726
categories:
  - Default Category
date: 2016-01-11 22:17:55
---

clipped alignment因为着在比对过程中，并没有用到全部的read的序列，read两段的序列被截取了（clip or trim）。如下表示，即为clip alignment。

Alignment:

```
Read:          ACGGTTGCGTTAA-TCCGCCACG
|                           ||||||||| ||||||
Reference: TAACTTGCGTTAAATCCGCCTGG
```




与clipped alignment对应的是spliced alignment，即read的中间没有比对到而两段比对上了。对应的表示如下：

Alignment:

```
Read:          ACGGTTGCGTTAAGCTCATCCGCCACG
|                 |||||||||||||         |||||||||
Reference: ACGGTTGCGTTAA…..TCCGCCACG
```





clip alignment对应的CIGAR表示有两种S （soft clip） 和H （hard clip）。
BWA提到If the read has a chimeric alignment, the paired or the top hit uses soft clipping and is marked with neither 0x800 nor 0x100 bits. All the other hits part of the chimeric alignment will use hard clipping and be marked with 0x800 if option "-M" is not in use, or marked with 0x100 otherwise.

即如果发现嵌合比对，最好的比对top hit标记为soft clipping，其余的则标记为hard clipping。

如果是hard clip，则截取的部分不会在SAM文件对应的read中出现 (clipped sequences not present in SEQ)，如果是soft clip (clipped sequences present in SEQ)，则会出现。

Understand？

Ref：https://github.com/lh3/bwa/blob/master/NEWS.md

\#####################################################################
\#版权所有 转载请告知 版权归作者所有 如有侵权 一经发现 必将追究其法律责任
\#Author: Jason
\#####################################################################