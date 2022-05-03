---
title: Get the reference allele based on genomic position
tags:
  - Base
  - UCSC
url: archives/739/index.html
id: 739
categories:
  - Default Category
date: 2016-02-24 21:17:26
---

This post will show how to get the reference base of chr1 from 49999 to 500001 (Version: hg19).
Please note: different tools has different coordinate (0 start or 1 start).

## 1, SAMtools

Index reference sequence in the FASTA format or extract subsequence from indexed reference sequence. If no region is specified, faidx will index the file and create .fai on the disk. If regions are specified, the subsequences will be retrieved and printed to stdout in the FASTA format.

```
$samtools faidx ucsc.hg19.fasta chr1:49999-50001
>chr1:49999-50001
ATA
```




## 2, twoBitToFa 

```
$wget http://hgdownload.soe.ucsc.edu/admin/exe/linux.x86_64/faToTwoBit
$wget http://hgdownload.soe.ucsc.edu/admin/exe/linux.x86_64/twoBitToFa
$chmod 755 twoBitToFa faToTwoBit 
$faToTwoBit ucsc.hg19.fasta ucsc.hg19.2bit
$twoBitToFa ucsc.hg19.2bit -seq=chr1 -start=49998 -end=50001 temp.out && cat temp.out && rm temp.out
>chr1:49998-50001
ATA
```

## 3, UCSC DAS server

```
$wget -qO- http://genome.ucsc.edu/cgi-bin/das/hg19/dna?segment=chr1:49999,50001 | grep -v '<'
ata
```

<!--more-->

## 4, bedtools getfasta

```
$bedtools getfasta -fi ucsc.hg19.fasta -bed test.bed -fo -
>chr1:49998-50001
ATA
```

## 5, UCSC UCSC Genome Browser

just input the chr and position in UCSC genome browser.
[http://genome.ucsc.edu/cgi-bin/hgTables](http://genome.ucsc.edu/cgi-bin/hgTables "http://genome.ucsc.edu/cgi-bin/hgTables")

## 6，togows

[http://togows.org/ ](http://togows.org/ "http://togows.org/ ")
TogoWS was originally developed to realize uniformed REST services over the public REST and SOAP services provided by NCBI, EBI, DDBJ, PDB, and KEGG. Because most of those SOAP services were discontinued in 2012, we then focus on providing intuitive REST APIs, inclusion of UCSC genome databases and support for the Semantic Web.

```
$wget http://togows.org/api/ucsc/hg19/chr1:49999-50001.fasta -O - -q
>hg19:chr1:49999-50001
ATA
```

And many other usful tools can make it. If you have a good idea, make a comment below.

Reference:
http://www.htslib.org/doc/samtools.html
https://genome.ucsc.edu/goldenpath/help/twoBit.html
https://www.biostars.org/p/19267/
http://bedtools.readthedocs.org/
https://www.biostars.org/p/56/

\#####################################################################
\#版权所有 转载请告知 版权归作者所有 如有侵权 一经发现 必将追究其法律责任
\#Author: Jason
\####################################################################