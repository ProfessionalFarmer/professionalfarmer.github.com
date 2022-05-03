---
title: How to extract paired-end reads from SRA files（reprint）
tags:
  - SRA
url: archives/705/index.html
id: 705
categories:
  - Default Category
date: 2013-06-20 21:29:02
---

SRA(NCBI) stores all the sequencing run as single "sra" or "lite.sra" file. You may want separate files if you want to use the data from paired-end sequencing. When I run SRA toolkit's "fastq-dump" utility on paired-end sequencing SRA files, sometimes I get only one files where all the mate-pairs are stored in one file rather than two or three files. The solution for the problem is to always run fastq-dump with "-split-3" option. If the experiment is single-end sequencing, only one fastq file will be generated. If it is paired-end sequencing, there may be two or three fastq files. Two files (with suffix "1" and "2") are matched mate-pair read file where as the third one (without any suffix) contains all the reads that do not have any mate-paires (or SRA couldn't resolve mate-paires for them).

Hope my experiences with NCBI SRA data handling help the readership.

source：[http://vinaykmittal.blogspot.com/2012/02/how-to-extract-paired-end-reads-from.html ](http://vinaykmittal.blogspot.com/2012/02/how-to-extract-paired-end-reads-from.html)

SRA toolkit document：[http://www.ncbi.nlm.nih.gov/Traces/sra/sra.cgi?view=toolkit_doc&f=fastq-dump ](http://www.ncbi.nlm.nih.gov/Traces/sra/sra.cgi?view=toolkit_doc&f=fastq-dump)

An example command:

`./fastq-dump.2 -split-3 ~/Desktop/ERR068552.sra -O ~/Desktop/temp.fastaq/`

PS: 如果测序使用的是ligation，结果为2 base encoding的color-space reads，可以加入-B选项使得fastq中的序列为base space reads

