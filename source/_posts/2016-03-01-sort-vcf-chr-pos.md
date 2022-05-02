---
title: Sort VCF by Chr and Pos根据染色体位置对VCF进行排序
tags:
  - VCF
url: archives/741.html
id: 741
categories:
  - Default Category
date: 2016-03-01 21:53:23
---

对VCF文件中的突变按照染色体和位置进行排序，下面是本人的总结，其中利用bash命令的方法不依赖其他的工具或包。htslib[前文](http://wp.zxzyl.com/?p=189 "合并VCF文件 Merge VCF file")中也提到过。

## 1, Use bash

**bash raw.vcf**

```
chr_order="chrMnchr1nchr2nchr3nchr4nchr5nchr6nchr7nchr8nchr9nchr10nchr11nchr12nchr13nchr14nchr15nchr16nchr17nchr18nchr19nchr20nchr21nchr22nchrXnchrY"

cat "$1" ' grep "^#" > .header.vcf
cat "$1" ' grep -v "^#" ' sort -k1,1 -k2,2n > .pre.sorted.vcf
echo -e $chr_order ' while read line
do
    cat .pre.sorted.vcf ' grep "^$line"$'t' >> .header.vcf
done
mv .header.vcf  sorted.vcf && rm .header.vcf .pre.sorted.vcf
```


## 2，Use awk and sed

(awk '/^#/{print}!/^#/{exit}' raw.vcf;sed '/^#/d' raw.vcf'awk -F"\t" '($1~/^[0-9]+$/){sub("^chr","",$0);print $0}''sort -k1,1n -k2,2n'awk '{print "chr"$0}' ;sed '/^#/d' raw.vcf' awk -F"\t" '($1!~/^[0-9]+$/){sub("^chr","",$0);print $0}''sort -k1,1d -k2,2n'awk '{print "chr"$0}') > sort.vcf

## 3, Use Picard

Sorts one or more VCF files. This tool sorts the records in VCF files according to the order of the contigs in the header/sequence dictionary and then by coordinate. It can accept an external sequence dictionary.

`java -jar picard.jar SortVcf I=unsort.vcf O=sorted.vcf`

## 4，Use vcf-sort (in vcftools)

`cat file.vcf  '  vcf-sort > sorted.vcf`
<!--more-->

## 5, Use htslib

```
chr_order="chrM chr1 chr2 chr3 chr4 chr5 chr6 chr7 chr8 chr9 chr10 chr11 chr12 chr13 chr14 chr15 chr16 chr17 chr18 chr19 chr20 chr21 chr22 chrX chrY"

cat "$1" ' grep "^#" > .pre.sorted.vcf
cat "$1" ' grep -v "^#" ' sort -k1,1 -k2,2n  >> .pre.sorted.vcf
bgzip -c .pre.sorted.vcf > .pre.sorted.vcf.gz
tabix -f -p vcf .pre.sorted.vcf.gz
tabix -H .pre.sorted.vcf.gz > .sort.vcf
echo -e $chr_order ' xargs tabix -h .pre.sorted.vcf.gz >> .sort.vcf
mv .header.vcf  sorted.vcf && rm .pre.sorted.vcf.gz .pre.sorted.vcf .sort.vcf
```

## How to install htslib

```bash
wget https://github.com/samtools/htslib/releases/download/1.3/htslib-1.3.tar.bz2
tar -jxvf htslib-1.3.tar.bz2
cd htslib-1.3
autoconf       # Generate the configure script, if needed
./configure    # Optional, needed for choosing optional functionality
make
make prefix=/path/to/install install
```

## How to install vcftools

```
git clone https://github.com/vcftools/vcftools.git
cd vcftools/ 
./autogen.sh 
./configure 
make 
make install
```

## Ref：

[https://www.biostars.org/p/84747/](https://www.biostars.org/p/84747/ "https://www.biostars.org/p/84747/")

[http://broadinstitute.github.io/picard/command-line-overview.html#SortVcf](http://broadinstitute.github.io/picard/command-line-overview.html#SortVcf "http://broadinstitute.github.io/picard/command-line-overview.html#SortVcf")

[https://github.com/samtools/htslib](https://github.com/samtools/htslib "https://github.com/samtools/htslib")

[http://vcftools.sourceforge.net/perl_module.html#vcf-sort](http://vcftools.sourceforge.net/perl_module.html#vcf-sort "http://vcftools.sourceforge.net/perl_module.html#vcf-sort")

\#####################################################################
\#版权所有 转载请告知 版权归作者所有 如有侵权 一经发现 必将追究其法律责任
\#Author: Jason
\####################################################################