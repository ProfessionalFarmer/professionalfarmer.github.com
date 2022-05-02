---
title: EBI提供HLA序列BLAST
tags:
  - Blast
  - HLA
url: archives/1032.html
id: 1032
categories:
  - Default Category
date: 2018-09-14 15:08:57
---


基于我们有的HLA序列，可以和HLA序列的数据库比较，看与哪个HLA allele最相似。

HLA （human leukocyte antigen，人类白细胞抗原）是人类主要组织相容性复合体（major histocompatibility complex，MHC）的表达产物，根据HLA抗原结构、功能及组织分布的不同，分为I类，II类，III类分子，其中I类分子包括HLA-A，-B，-C系列抗原，广泛分布于各组织有核系统表面。

BLAST表示局部比对搜索工具，用来将新的序列与已有的数据库中的序列进行比较，可以发现区域的相似性，进而为功能和进化研究提供线索。
EBI（欧洲生物信息学中心）提供基于IPD-IMGT/HLA（IMGT国际免疫遗传学数据库）数据库的BLAST库。BLAST工具会搜索数据库中的HLA allele的核苷酸、蛋白质及相关对的序列。

HLA BLAST在线服务的链接如下：
[https://www.ebi.ac.uk/Tools/services/web_ncbiblast/toolform.ebi?tool=ncbiblast&context=nucleotide&database=imgthla](https://www.ebi.ac.uk/Tools/services/web_ncbiblast/toolform.ebi?tool=ncbiblast&context=nucleotide&database=imgthla)

## 1）选择数据库

![](/wp/f4w/2020/2018-09-14-EBI-EMBL-HLA-BLAST1.png) 

选择IMGT下的IMGT/HLA (genomic)数据据，表示与HLA的基因组序列进行比对，如果需要和编码区序列进行比对，可以选择IMGT/HLA (cds)。

## 2）输入待比对的序列

BLAST支持简并碱基的比对，比如用R表示G或A (puRine)，用A表示M表示A或C。

## 3）设置参数

![](/wp/f4w/2020/2018-09-14-EBI-EMBL-HLA-BLAST3.png)

选择blastn表示进行核苷酸序列比对，task可以用megablast也可以用blastn，其他参数可以选择默认。

## 4）提交任务

点击submit提交任务。

## 5）等待结果

一般情况下，会在10秒左右进入比对结果页面。结果页面包含相似性和显著性结果。

## 测试序列

```
CGAACTTGGCGGGTCTCAGCCCTCCTSGCCCCAGGCTCCCACTCCATGAGGTATTTCTACACCGCCATGTCCCGGCCCGG
CCGCGGGGAGCCCCGCTTCATCRCMGTGGGCTACGTGGACGACACSCAGTTCGTGMGGTTCGACAGCGACGCCRCGAGTC
CGAGRRKGGMGCCSCGGGCGCCRTGGRTRGAGCAGGAGGGGCCGGAGTATTGGGACCGGAASACACAGATCTMCAAGGCC
MASGCACAGACTGACCGAGAGAACCTGCGSAACCTGCTCGGCTACTACAACCAGAGCGAGGCCGGTGAGTGACCCCGGCC
CGGGGCGCAGGTCACGACTCCCCATCCCCCACGKACGGCCCGGGTCGCCCCGAGTCTCCGGGTCCGAGATCCGCCTCCCT
GAGGCCGCGGGACCCGCCCAGACCCTCGACCGGCGAGAGCCCCAGGCGCGTTTACCCGGTTTCATTTTCAGTTGAGGCCA
AAATCCCCGCGGGTTGGTCGGGGCGGGGCGGGGCTCGGGGGACGGGGCTGACCGCGGGGCCGGGGCCAGGGTCTCACACT
TGGCAGACGATGTATGGCTGCGACCTGGGGCCGGACGGGCGCCTCCTCCGCGGGCATAACCAGTTAGCTACGACGGCAGG
```




该序列的测试结果，与本地blast的结果一致。

## 参考：

[https://www.ebi.ac.uk/ipd/imgt/hla/blast.html](https://www.ebi.ac.uk/ipd/imgt/hla/blast.html)

\#####################################################################
\#版权所有 转载请告知 版权归作者所有 如有侵权 一经发现 必将追究其法律责任
\#Author: Jason
\#####################################################################