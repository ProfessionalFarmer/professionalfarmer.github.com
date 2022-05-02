---
title: 基于DNA或RNA的NGS数据进行HLA分型
tags:
  - NGS
  - HLA
url: archives/1113.html
id: 1113
categories:
  - Default Category
date: 2020-06-14 23:09:11
---


写这个原因呢，最近又要对样本的HLA分子进行分型，然后看到某公司的微信公众号讲的HLA的分型软件，全文讲了那么多，要么巨难用，要么下载不到，反正不如我自己正在用的这两个。另外一方面，没必要太纠结非常高的精度，除非你用得到。4-digital resolution，我觉得已经够了。

# HLA分子

先回顾下百度百科对HLA的介绍（https://baike.baidu.com/item/HLA/9504270?fr=aladdin）：

HLA(human leukocyte antigen ，人类白细胞抗原)是人类的主要组织相容性复合体（MHC）的表达产物，该系统是所知人体最复杂的多态系统。

HLA是具有高度多态性的同种异体抗原，其化学本质为一类糖蛋白，由一条α重链（被糖基化的）和一条β轻链非共价结合而成。其肽链的氨基端向外（约占整个分子的3/4），羧基端穿入细胞质，中间疏水部分在胞膜中。HLA按其分布和功能分为Ⅰ类抗原和Ⅱ类抗原。

HLA-I类分子：内源性抗原的递呈分子，  HLA-Ⅱ类分子：外源性抗原的递呈分子

# 我想介绍的是seq2hla和optitype这两个软件

软件的大致原理，都是和HLA数据库中的数据进行比对，然后分型。我拿过7个样本的RNA数据用这两个软件进行比较，如下表，虽然个别分型不一致（后两个resolution不一致），但大部分结果还是相当一致的。

| SAMPLE    |                 |     A1         |     A2         |     B1          |     B2          |     C1         |     C2         |
|-----------|-----------------|----------------|----------------|-----------------|-----------------|----------------|----------------|
| 1         |     seq2HLA     |     A*02:01    |     A*24:18    |     B*35:102    |     B*35:102    |     C*16:02    |     C*04:01    |
|           |     OptiType    |     A*02:01    |     A*24:02    |     B*35:14     |     B*35:14     |     C*16:02    |     C*04:01    |
| 2         |     seq2HLA     |     A*29:01    |     A*02:07    |     B*46:01     |     B*15:01     |     C*04:01    |     C*01:02    |
|           |     OptiType    |     A*29:01    |     A*02:07    |     B*46:01     |     B*15:01     |     C*04:01    |     C*01:02    |
| 3         |     seq2HLA     |     A*02:07    |     A*11:01    |     B*52:01     |     B*15:01     |     C*12:02    |     C*03:03    |
|           |     OptiType    |     A*02:07    |     A*11:01    |     B*52:01     |     B*15:01     |     C*12:02    |     C*03:03    |
| 4         |     seq2HLA     |     A*02:07    |     A*11:01    |     B*46:01     |     B*40:01     |     C*01:02    |     C*07:02    |
|           |     OptiType    |     A*02:07    |     A*11:01    |     B*46:01     |     B*40:01     |     C*01:02    |     C*07:02    |
| 5         |     seq2HLA     |     A*33:03    |     A*11:01    |     B*58:01     |     B*15:02     |     C*03:02    |     C*08:01    |
|           |     OptiType    |     A*33:03    |     A*11:01    |     B*58:01     |     B*15:02     |     C*03:02    |     C*08:01    |
| 6         |     seq2HLA     |     A*02:07    |     A*29:01    |     B*46:01     |     B*07:02     |     C*01:02    |     C*15:05    |
|           |     OptiType    |     A*02:07    |     A*29:01    |     B*46:01     |     B*07:05     |     C*01:02    |     C*15:05    |
| 7         |     seq2HLA     |     A*02:03    |     A*11:01    |     B*56:01     |     B*56:01     |     C*01:02    |     C*01:02    |
|           |     OptiType    |     A*02:03    |     A*11:01    |     B*56:01     |     B*56:01     |     C*04:01    |     C*01:02    |


# seq2hla

首先介绍的是seq2hla，这个其实一个命令就可以进行HLA的分型（很实用吧），但只基于RNA Seq的数据，我见有人用WES的数据来做，但不确定靠不靠谱。

官网： https://bitbucket.org/sebastian_boegel/seq2hla/wiki/Home

## 利用conda安装

```
conda create -n seq2hla
conda install -n seq2hla -c bioconda seq2hla
```

## 运行

```
seq2HLA -1  readfile1  -2  readfile2  -r  runname  [-p int] [-3 int]
# 提供R1和R2，现在已经支持gzip格式，-p是线程，-3是trim read末端的碱基数（因为read末端的碱基质量不高）
```

## seq2hla的结果

下面的结果基于RNA-seq的数据得到的，在介绍optitype的时候，我用的是WES-seq的数据，可以看到虽然软件和数据类型不同，但两个软件的结果是一致的，综合前面表格中两种软件基于同一样本RNA-seq的结果，和两种软件基于同一样本不同数据类型的结果来看，都能说明两个软件都比较靠谱。

```
#Locus  Allele 1        Confidence      Allele 2        Confidence
A       A*24:02 0.001426754     A*11:01 0.003463472
B       B*38:02'        0.0002728549    B*46:01 0.0002107604
C       C*01:02 0.01282529      C*07:02 0.01516768
#Locus  Allele 1        Confidence      Allele 2        Confidence
DQA     no      NA      no      NA
DQB     DQB1*05:02      NA      DQB1*05:02      NA
DRB     DRB1*11:52      0.297521        DRB1*04:05'     0.42202
```

# optitype

另外一个软件是optitype，这个软件呢，稍微多了几步，但绝对在让人接受的范围内，而且这个软件支持DNA数据和RNA数据。

官网：https://github.com/FRED-2/OptiType

## 利用conda安装

这个时候真的要安利下conad，有了conda之后，各种软件包的安装和管理，变得非常轻松。拿optitype来说，我第一次安装的时候，自己下载，编译，修改部分文件，还要自己安装razers，而有了conda之后，只需一个命令

```
conda create -n optitype
conda install -n optitype -c bioconda optitype
```

optitype需要先利用razers3先过滤一下reads，把和HLA相关的序列提出来，然后在运行optitype进行分型，从而加快分析速度。

## 第一步，Razers3
```
razers3 -i 95 -m 1 -dr 0 --thread-count 10 -o fished_1.bam /path/to/hla_reference_dna.fasta sample_1.fastq
```

我是用conda装的，但在conda的env目录下没找到hla的fasta文件，不过不用着急，官网上有，可以从 https://github.com/FRED-2/OptiType/tree/master/data 下载对应的HLA的DNA或RNA的数据。

如果是paired的read，则需要分别跑一次，得到fished_1.bam和fished_2.bam文件。

另外官网提示Razers3会把所有的fastq读到内容，所以计算服务器的内存最好大点。

## 第二步，将bam文件转成fastq

```
samtools bam2fq fished_1.bam > fished_1.fastq
samtools bam2fq fished_2.bam > fished_2.fastq
```

## 第三步，运行optitype
```
OptiTypePipeline.py -i fished_1.fastq fished_2.fastq --dna -v -o /path/to/outdir -p sample.optitype.dna
```

–dna需要和前面Razers3用的HLA的序列类型一致，如果前面用的RNA的数据，这里也是–rna，当然用RNA还是DNA取决于测序数据。

optitype的结果
这个结果和seq2hla基于RNA-seq的数据得到的HLA亚型是一致的。

```
        A1      A2      B1      B2      C1      C2      Reads   Objective
0       A*11:01 A*24:02 B*38:02 B*46:01 C*01:02 C*07:02 200.0   191.00000000000003
```

#####################################################################
#版权所有 转载请告知 版权归作者所有 如有侵权 一经发现 必将追究其法律责任
#Author: Jason
#####################################################################

