---
title: SAMtools自带的统计命令--idxstats、stat、flagstat、bedcov和depth命令
tags:
  - SAM
  - stat
url: archives/727/index.html
id: 727
categories:
  - Default Category
date: 2016-01-11 22:51:33
---
**SAMtools**不仅仅用来call snp。从samtools的软件名就能看出，是对SAM格式文件进行操作的工作，比如讲sam转成bam格式，index，rmdup等等。samtools结合linux命令比如grep，awk和SAM格式描述的flag，tag，亦是非常非常非常强大，比如根据flag过滤duplicate的reads，根据XA tag过滤multiple hit的reads。本文在此只介绍一下samtools的统计命令，能快速对bam文件进行各种统计。

samtools的自带的几种统计工具

**samtool idxstats **

检索和打印与输入文件相对应的index file里的统计信息，所以要对输入的bam文件进行index

reference sequence name, sequence length, # mapped reads and # unmapped reads
chr1    249250621       4998344 1005
chr2    243199373       3020248 595
chr3    198022430       2418804 449

**samtools bedcov**

计算覆盖到每个区域的总碱基数目

chr    start-1    end    totalbase
chr1    100000  1000000 1709228
chr2    2000000 65885852        64362582

**samtools depth **

计算每个位点的深度

\#chr    pos     depth
chr1    1       5
chr1    2       5

**samtools flagstat**

根据flag统计多少map的reads等信息
43444444 + 0 in total (QC-passed reads + QC-failed reads)
5863846 + 0 secondary
0 + 0 supplementary
0 + 0 duplicates
43431948 + 0 mapped (99.97%:-nan%)
37580598 + 0 paired in sequencing
<!--more-->

**samtools stat bamfile**

输出的信息比较多，部分如下

Summary Numbers
raw total sequences，filtered sequences, reads mapped, reads mapped and paired,reads properly paired等信息

Fragment Qualitites
根据cycle统计每个位点上的碱基质量分布

Coverage distribution
深度为1，2，3，，，的碱基数目

ACGT content per cycle
ACGT在每个cycle中的比例

Insert sizes
插入长度的统计

Read lengths
read的长度分布

参考SAMtools的官网提供的document:
http://www.htslib.org/doc/samtools.html

**idxstats**

`samtools idxstats in.sam'in.bam'in.cram`

Retrieve and print stats in the index file corresponding to the input file. Before calling idxstats, the input BAM file must be indexed by samtools index.

The output is TAB-delimited with each line consisting of reference sequence name, sequence length, # mapped reads and # unmapped reads. It is written to stdout.

**flagstat**

`samtools flagstat in.sam'in.bam'in.cram`

Does a full pass through the input file to calculate and print statistics to stdout.

Provides counts for each of 13 categories based primarily on bit flags in the FLAG field. Each category in the output is broken down into QC pass and QC fail, which is presented as "#PASS + #FAIL" followed by a description of the category.

The first row of output gives the total number of reads that are QC pass and fail (according to flag bit 0x200). For example:

122 + 28 in total (QC-passed reads + QC-failed reads)

Which would indicate that there are a total of 150 reads in the input file, 122 of which are marked as QC pass and 28 of which are marked as "not passing quality controls"

Following this, additional categories are given for reads which are:

secondary
0x100 bit set

supplementary
0x800 bit set

duplicates
0x400 bit set

mapped
0x4 bit not set

paired in sequencing
0x1 bit set

read1
both 0x1 and 0x40 bits set

read2
both 0x1 and 0x80 bits set

properly paired
both 0x1 and 0x2 bits set and 0x4 bit not set

with itself and mate mapped
0x1 bit set and neither 0x4 nor 0x8 bits set

singletons
both 0x1 and 0x8 bits set and bit 0x4 not set

And finally, two rows are given that additionally filter on the reference name (RNAME), mate reference name (MRNM), and mapping quality (MAPQ) fields:

with mate mapped to a different chr
0x1 bit set and neither 0x4 nor 0x8 bits set and MRNM not equal to RNAME

with mate mapped to a different chr (mapQ>=5)
0x1 bit set and neither 0x4 nor 0x8 bits set and MRNM not equal to RNAME and MAPQ >= 5

**stats**

```samtools stats [options] in.sam'in.bam'in.cram [region...]```

samtools stats collects statistics from BAM files and outputs in a text format. The output can be visualized graphically using plot-bamstats.

Options:

-c, --coverage MIN,MAX,STEP
Set coverage distribution to the specified range (MIN, MAX, STEP all given as integers) [1,1000,1]

-d, --remove-dups
Exclude from statistics reads marked as duplicates

-f, --required-flag STR'INT
Required flag, 0 for unset. See also `samtools flags` [0]

-F, --filtering-flag STR'INT
Filtering flag, 0 for unset. See also `samtools flags` [0]

--GC-depth FLOAT
the size of GC-depth bins (decreasing bin size increases memory requirement) [2e4]

-h, --help
This help message

-i, --insert-size INT
Maximum insert size [8000]

-I, --id STR
Include only listed read group or sample name []

-l, --read-length INT
Include in the statistics only reads with the given read length []

-m, --most-inserts FLOAT
Report only the main part of inserts [0.99]

-P, --split-prefix STR
A path or string prefix to prepend to filenames output when creating categorised statistics files with -S/--split. [input filename]

-q, --trim-quality INT
The BWA trimming parameter [0]

-r, --ref-seq FILE
Reference sequence (required for GC-depth and mismatches-per-cycle calculation). []

-S, --split TAG
In addition to the complete statistics, also output categorised statistics based on the tagged field TAG (e.g., use --split RG to split into read groups).

Categorised statistics are written to files named\ _.bamstat, where prefix is as given by --split-prefix (or the input filename by default) and value has been encountered as the specified tagged field's value in one or more alignment records.

-t, --target-regions FILE
Do stats in these regions only. Tab-delimited file chr,from,to, 1-based, inclusive. []

-x, --sparse
Suppress outputting IS rows where there are no insertions.

**bedcov**

`samtools bedcov region.bed in1.sam'in1.bam'in1.cram[...]`

Reports read depth per genomic region, as specified in the supplied BED file.

**depth**

`samtools depth [options] [in1.sam'in1.bam'in1.cram [in2.sam'in2.bam'in2.cram] [...]]`

Computes the depth at each position or region.

Options:

-a
Output all positions (including those with zero depth)

-a -a, -aa
Output absolutely all positions, including unused reference sequences

-b FILE
Compute depth at list of positions or regions in specified BED FILE. []

-f FILE
Use the BAM files specified in the FILE (a file of filenames, one file per line) []

-l INT
Ignore reads shorter than INT

-m, -d INT
Truncate reported depth at a maximum of INT reads. [8000]

-q INT
Only count reads with base quality greater than INT

-Q INT
Only count reads with mapping quality greater than INT

-r CHR:FROM-TO
Only report depth in specified region.

Ref:http://www.htslib.org/doc/samtools.html

\#####################################################################
\#版权所有 转载请告知 版权归作者所有 如有侵权 一经发现 必将追究其法律责任
\#Author: Jason Zhu
\#####################################################################