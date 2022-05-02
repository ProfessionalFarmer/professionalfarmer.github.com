---
title: 合并VCF文件 Merge VCF file
tags:
  - VCF
url: archives/740.html
id: 740
categories:
  - Default Category
date: 2016-02-29 20:47:58
---

VCF为variant call file格式，现为标准的SNV突变存储格式。通常情况下，一个VCF文件对应一个样本的突变。但VCF格式同样支持同时在一个文件中表示多个样本的突变，在每一行的最后几列，每一列代表一个样本在特定位点的突变情况，若样本在该位点没有突变，在代表样本的那一列在该位点的记录为.点号。
此外，在生成VCF的时候，可以生成包含多个样本突变的VCF。但是要在序列比对生成SAM文件时要加入SM tag用来指定哪些reads属于哪个样本。

多个样本的突变情况用一个VCF文件存储的好处在于，对于发生突变的特定位点，可以迅速了解不同样本在该位点的突变情况。比如下列，最后三列表示三个样本在染色体chrT的525位点的突变情况，

```
#对应GT:PL:GQ:AD:DP。其中第一个样本在该位点没有发生突变，第二个样本的基因型为C/C，第三个样本的基因型为G/T。
chrT    515    .    G    C,T    1230.23    PASS    AC=4;AF=1.00;AN=4;DP=76;FS=0.000;MLEAC=2;MLEAF=1.00;MQ0=0;MQ=60.24;QD=33.32;RPA=5,4;RU=CA;SF=1,2;SOR=0.793;STR;set=variant23    GT:PL:GQ:AD:DP    .    1/1:1570,120,0:99:0,40:46    0/2:965,69,0:69:0,23:30
```

## 一，vcftools

VCFtools is a program package designed for working with VCF files, such as those generated by the 1000 Genomes Project. The aim of VCFtools is to provide easily accessible methods for working with complex genetic variation data in the form of VCF files.

VCFtools的功能和SAMtools类似，用于处理VCF格式的文件，可用于合并VCF。

VCFtools的输入文件格式为gz格式，需要用bgzip压缩，并用tabix生成index文件。
tabix和bgzip在samtools安装包的htslib\-*文件夹中，需要单独安装。首先下载samtools（也可以专门下载htslib包，或者你已经有samtools，看是否有htslib文件夹），进入htslib文件夹中

```bash
wget https://github.com/samtools/htslib/releases/download/1.3/htslib-1.3.tar.bz2
tar -jxvf htslib-1.3.tar.bz2
cd htslib-1.3
./configure 
make
make prefix=/path/to/install install
```

### download vcftools，install vcftools

```
git clone https://github.com/vcftools/vcftools.git
cd vcftools/ 
./autogen.sh 
./configure 
make 
make install
```

### compress, index and merge VCF

```
bgzip -c "x.vcf" > "x.vcf.gz"
bgzip -c "y.vcf > "y.vcf.gz"
bgzip -c "z.vcf" > "z.vcf.gz"
tabix -f "x.vcf.gz"
tabix -f "y.vcf.gz"
tabix -f "z.vcf.gz"
vcf_merge   x.vcf.gz   y.vcf.gz   z.vcf.gz  > merged.vcf
```

<!--more-->

## 二，GATK的CombineVariants工具

GATK在合并VCF时，需要用到参考基因组文件，并且有对应的dict文件。如果没有（一般进行call SNP或者比对的时候，都会用到dict），请先用picard的生成。

```
java -Xms2g -jar picard.jar CreateSequenceDictionary R=primary_assembly.sort.fa O=primary_assembly.sort.dict
java -Xms2g -jar GenomeAnalysisTK.jar -T CombineVariants -R primary_assembly.sort.fa --variant x.vcf --variant .yvcf --variant z.vcf -o merged.vcf -genotypeMergeOptions UNIQUIFY
```

参考：
[https://vcftools.github.io/index.html](https://vcftools.github.io/index.html "https://vcftools.github.io/index.html")

[https://www.broadinstitute.org/gatk/guide/tooldocs/org_broadinstitute_gatk_tools_walkers_variantutils_CombineVariants.php](https://www.broadinstitute.org/gatk/guide/tooldocs/org_broadinstitute_gatk_tools_walkers_variantutils_CombineVariants.php "https://www.broadinstitute.org/gatk/guide/tooldocs/org_broadinstitute_gatk_tools_walkers_variantutils_CombineVariants.php")

\#####################################################################
\#版权所有 转载请告知 版权归作者所有 如有侵权 一经发现 必将追究其法律责任
\#Author: Jason
\####################################################################