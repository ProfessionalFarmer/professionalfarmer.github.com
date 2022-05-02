---
title: ControlFreec检测CNV
tags:
  - CNV
url: archives/717.html
id: 717
categories:
  - Default Category
date: 2015-12-11 21:34:40
---

1,下载control freec

地址：[http://bioinfo-out.curie.fr/projects/freec/src/FREEC_Linux64.tar.gz](http://bioinfo-out.curie.fr/projects/freec/src/FREEC_Linux64.tar.gz "http://bioinfo-out.curie.fr/projects/freec/src/FREEC_Linux64.tar.gz")

2，编译

    tar -zxvf FREEC_Linux64.tar.gz
    make

3，control freec根据配置文件进行工作，运行control freec之前需要进行的准备工作有
<!--more-->

1）生成配置参数chrLenFile对应的文件hg19.len，储存染色体长度，具体格式和内容可以直接拷贝[http://bioinfo-out.curie.fr/projects/freec/src/hg19.len](http://bioinfo-out.curie.fr/projects/freec/src/hg19.len "http://bioinfo-out.curie.fr/projects/freec/src/hg19.len")

2）生成配置参数chrFiles对应的文件夹，/path/to/grch_chr，文件夹内里面包含1.fa, 2.fa.....,文件名必须以染色体为单位和开头

```bash
for i in {1..22};
do gunzip -c /path/to/Homo_sapiens.GRCh37.75.dna.chromosome.$i.fa.gz >$i.fa;
done
do gunzip -c /path/to/Homo_sapiens.GRCh37.75.dna.chromosome.X.fa.gz >X.fa;
do gunzip -c /path/to/Homo_sapiens.GRCh37.75.dna.chromosome.Y.fa.gz >Y.fa;
```

3）在没有对照样本的情况下，chrFiles和GCcontentProfile必须配置，第二步已经生成了chrFiles对应的文件夹，此步用于生成配置参数GCcontentProfile对应的文件

下载http://bioinfo-out.curie.fr/projects/freec/src/gccount.tar.gz，解压并编译

编写gccount的配置文件test.conf，gccount和freec可以共用配置文件，配置文件内容如下

```
[general]
##染色体长度，在2）生成
chrLenFile = ./hg19.len
##基因组倍数
ploidy = 2
##检测CNV的window size
window = 50000
##输出文件夹
outputDir = ./
##在2）步中生成
chrFiles = /path/to/grch_chr
```


运行gccount -conf test.conf会生成GC_profile.cnp文件，该文件对应配置参数GCcontentProfile

4)配置参数samtools对应的samtools路径

下载samtools，地址[https://github.com/samtools/samtools/releases/latest/](https://github.com/samtools/samtools/releases/latest/ "https://github.com/samtools/samtools/releases/latest/")

```
tar -jvxf samtools.tar.bz2
cd samtools-1.2
make
make prefix=/where/to/install install
```

4，编写运行freec的配置文件

```
[general]
##染色体长度，在第一步生成
chrLenFile = ./hg19.len
##基因组倍数
ploidy = 2
##检测CNV的window size
window = 50000
##输出文件夹
outputDir = ./
##在第二步中生成
chrFiles = /path/to/grch_chr
##第3.3）步生成
GCcontentProfileGC_profile.cnp
##第3.4）步samtools的绝对路径
samtools=/path/to/samtools-1.2/samtools

[sample]
mateFile = /path/to/sample.bam
inputFormat = BAM
```



## illumina pair end
mateOrientation = FR</pre>

5，运行freec

`freec -conf test.conf`

会在outputDir生成sample.bam_CNVs等文件。

文件格式参见：[http://bioinfo-out.curie.fr/projects/freec/tutorial.html#OUTPUT](http://bioinfo-out.curie.fr/projects/freec/tutorial.html#OUTPUT "http://bioinfo-out.curie.fr/projects/freec/tutorial.html#OUTPUT")

参考文档：http://bioinfo-out.curie.fr/projects/freec/tutorial.html

\#########################################################################
\#版权所有 转载请告知 版权归作者所有 如有侵权 一经发现 必将追究其法律责任
\#########################################################################