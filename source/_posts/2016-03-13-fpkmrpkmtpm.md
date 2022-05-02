---
title: 'FPKM,RPKM,TPM  转载'
tags:
  - RNA
  - Seq
url: archives/743.html
id: 743
categories:
  - Default Category
date: 2016-03-13 10:32:21
---

FPKM：Fragmentsper Kilobase Million，FPKM意义与RPKM极为相近。二者区别仅在于，Fragment 与Read。RPKM的诞生是针对早期的SE测序，FPKM则是在PE测序上对RPKM的校正。只要明确​Reads 和Fragments的区别，RPKM和FPKM的概念便易于区分。Reads即是指下机后fastq数据中的每一条Reads，Fragments则是指每一段用于测序的核酸片段，在SE中，一个Fragments只测一条Reads，所以，Reads数与Fragments数目相等；在PE中，一个Fragments测两端，会得到2条Reads，但由于后期质量或比对的过滤，有可能一个Fragments的2条Reads最后只有一条进入最后的表达量分析。总之，对某一对Reads而言，这2条Reads只能算一个Fragments，所以，Fragment的最终数目是Reads的1到2倍之间。

在衡量基因表现量时，若是单纯以map到的read数来计算基因的表现 量，在统计上是一件相当不合理事，因为在随机抽样的情况下，序列较长的基因被抽到的机率本来就会比序列短的基因较高，如此一来，序列长的基因永远会被认为 表现量较高，而错估基因真正的表现量，所以Ali Mortazavi等人在2008年提出以RPKM在估计基因的表现量。

"Reads Per Kilobase Per Million Reads"​，即"每一百万条Reads中，对基因的每1000个Base而言，比对到该1000个base的Reads数"

It used to be when you did RNA-seq, you reported your results in RPKM (Reads Per Kilobase Million) or FPKM (Fragments Per Kilobase Million). However, TPM (Transcripts Per Million) is now becoming quite popular. Since there seems to be a lot of confusion about these terms, I thought I'd use a StatQuest to clear everything up.

These three metrics attempt to normalize for sequencing depth and gene length. Here's how you do it for RPKM:
Count up the total reads in a sample and divide that number by 1,000,000 - this is our "per million" scaling factor.
Divide the read counts by the "per million" scaling factor. This normalizes for sequencing depth, giving you reads per million (RPM)
Divide the RPM values by the length of the gene, in kilobases. This gives you RPKM.
<!--more-->

FPKM is very similar to RPKM. RPKM was made for single-end RNA-seq, where every read corresponded to a single fragment that was sequenced. FPKM was made for paired-end RNA-seq. With paired-end RNA-seq, two reads can correspond to a single fragment, or, if one read in the pair did not map, one read can correspond to a single fragment. The only difference between RPKM and FPKM is that FPKM takes into account that two reads can map to one fragment (and so it doesn't count this fragment twice).

TPM is very similar to RPKM and FPKM. The only difference is the order of operations. Here's how you calculate TPM:
Divide the read counts by the length of each gene in kilobases. This gives you reads per kilobase (RPK).
Count up all the RPK values in a sample and divide this number by 1,000,000. This is your "per million" scaling factor.
Divide the RPK values by the "per million" scaling factor. This gives you TPM.

So you see, when calculating TPM, the only difference is that you normalize for gene length first, and then normalize for sequencing depth second. However, the effects of this difference are quite profound.

When you use TPM, the sum of all TPMs in each sample are the same. This makes it easier to compare the proportion of reads that mapped to a gene in each sample. In contrast, with RPKM and FPKM, the sum of the normalized reads in each sample may be different, and this makes it harder to compare samples directly.

Here's an example. If the TPM for gene A in Sample 1 is 3.33 and the TPM in sample B is 3.33, then I know that the exact same proportion of total reads mapped to gene A in both samples. This is because the sum of the TPMs in both samples always add up to the same number (so the denominator required to calculate the proportions is the same, regardless of what sample you are looking at.)

With RPKM or FPKM, the sum of normalized reads in each sample can be different. Thus, if the RPKM for gene A in Sample 1 is 3.33 and the RPKM in Sample 2 is 3.33, I would not know if the same proportion of reads in Sample 1 mapped to gene A as in Sample 2. This is because the denominator required to calculate the proportion could be different for the two samples.

转载自[http://www.rna-seqblog.com/rpkm-fpkm-and-tpm-clearly-explained/](http://www.rna-seqblog.com/rpkm-fpkm-and-tpm-clearly-explained/)

[http://fhqdddddd.blog.163.com/blog/static/1869915420126173518426/](http://fhqdddddd.blog.163.com/blog/static/1869915420126173518426/)