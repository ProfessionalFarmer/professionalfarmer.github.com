---
title: 统计覆盖到某一区域的reads数目和reads的GC含量
tags:
  - BEDtools
  - GC content
url: archives/729/index.html
id: 729
categories:
  - Default Category
date: 2016-01-12 22:19:45
---
statistic GC content by interval. BED format file include arget interval information. BEDTool statistic read number and extract sequence, awk statistic GC content.

    bedtools map -a interval.bed -b sample.bam -c 10,10 -o count,concat | awk -v OFS="t" '{n=length($5); gc=gsub("[gcGC]", "", $5); print $1,$2,$3,$4,gc/n}'

思路：利用bedtools的map工具，首先找到map到interval.bed中的每个interval的reads的序列，然后统计这些序列中有多少GC。 

缺点是，该map找到的是覆盖到interval的reads的序列，有可能read有一半与interval重叠，但bedtools会把该reads的所有序列都提出来。 

PS：Bedtools是基因组特征genome feature比对工具，用起来非常非常的爽。