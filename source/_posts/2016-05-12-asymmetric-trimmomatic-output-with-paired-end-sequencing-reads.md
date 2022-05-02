---
title: Asymmetric trimmomatic output with paired-end sequencing reads
tags:
  - NGS
  - QC
url: archives/758.html
id: 758
categories:
  - Default Category
date: 2016-05-12 16:28:14
---

运行trimmomatic的默认参数
------------------

```java
java -jar trimmomatic.jar PE -threads 16 -phred33 sample_1.fastq sample_2.fastq sample_trimmed_paired_1.fastq.gz sample_trimmed_unpaired_1.fastq.gz sample_trimmed_paired_2.fastq.gz sample_trimmed_unpaired_2.fastq.gz ILLUMINACLIP:adapters/TruSeq3-PE-2.fa:2:30:10 LEADING:3 TRAILING:3 SLIDINGWINDOW:4:15 MINLEN:36
```

输出文件中
-----

sample\_trimmed\_unpaired\_1.fastq.gz是sample\_trimmed\_unpaired\_2.fastq.gz的十多倍，异常的大。1文件（forward reads）中unpaired reads非常多，显著多余2文件（reverse reads）中的unpaired reads。

原因是
---

After read-though has been detected by palindrome mode, and the adapter sequence removed, the reverse read contains the same sequence information as the forward read, albeit in reverse complement. For this reason, the default behaviour is to entirely drop the reverse read. 

reverse read被丢弃之后，导致forward read中unpaired read非常多，出现上述非对称结果。

ILLUMINCLIP的最后两个参数可以额外的，其中minAdpterLength的默认参数为8，keepBothReads的参数为FALSE 

ILLUMINACLIP:::::: 

设置这两个额外的参数后，输出文件中的unpaired 文件大小趋于正常。 

By specifying "true" for this parameter, the reverse read will also be retained, which may be useful e.g. if the downstream tools cannot handle a combination of paired and unpaired reads.

PS:
---

trimmmomatic默认认为下游处理工具可以处理paired和unpaired reads，所以在palindrome mode（回文模式？）中丢弃了相关reads，而日常工作中，我们常常只利用paired-end read，所以keepBothReads参数最好设置为TRUE。优化后的参数见下：

```java
java -jar trimmomatic.jar PE -threads 16 -phred33 sample_1.fastq sample_2.fastq sample_trimmed_paired_1.fastq.gz sample_trimmed_unpaired_1.fastq.gz sample_trimmed_paired_2.fastq.gz sample_trimmed_unpaired_2.fastq.gz ILLUMINACLIP:adapters/TruSeq3-PE-2.fa:2:30:10:8:TRUE LEADING:3 TRAILING:3 SLIDINGWINDOW:4:15 MINLEN:36
```

REF
---

[http://www.usadellab.org/cms/uploads/supplementary/Trimmomatic/TrimmomaticManual_V0.32.pdf](http://www.usadellab.org/cms/uploads/supplementary/Trimmomatic/TrimmomaticManual_V0.32.pdf) 

[http://seqanswers.com/forums/showthread.php?t=38068](http://seqanswers.com/forums/showthread.php?t=38068) 

[http://www.usadellab.org/cms/?page=trimmomatic](http://www.usadellab.org/cms/?page=trimmomatic) 

\##################################################################### 
\#版权所有 转载请告知 版权归作者所有 如有侵权 一经发现 必将追究其法律责任 
\#Author: Jason 
\####################################################################