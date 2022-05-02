---
title: Illumina下机FASTQ文件命名规则
tags:
  - FASTQ
  - Illumina
url: archives/805.html
id: 805
categories:
  - Default Category
date: 2018-02-01 13:30:16
---

FASTQ文件在Illumina下机数据文件夹**Data\Intensities\BaseCalls\**中，类似**SampleName_S1_L001_R1_001.fastq.gz（比如NTC_S11_L001_R1_001.fastq.gz）**

其中被下划线_分为了五个部分。

*   第一部分：SampleName，样本名，与上机时在Sample Sheet中填写的一致
*   第二部分：S1，S***，S后跟的数字与样本在Sample Sheet中的顺序一致，从1开始。不能分配到确定样本的read会归到S0（Undetermined_S0）
*   第三部分：L00*，泳道lane的编号
*   第四部分：R*，R1表示read1，R2表示read2。R1和R2为paired end reads。同一个样本的配对的FASTQ，只有这个地方不同
*   第五部分：001，通常为001
**Naming**
FASTQ files are named with the sample name and the sample number, which is a numeric assignment based on the order that the sample is listed in the sample sheet. 
**Example:**
Data\Intensities\BaseCalls\SampleName_S1_L001_R1_001.fastq.gz
• SampleName-The sample name provided in the sample sheet. If a sample name is not provided, the file name includes the sample ID, which is a required field in the sample sheet and must be unique.
• S1-The sample number based on the order that samples are listed in the sample sheet starting with 1. In this example, S1 indicates that this sample is the first sample listed in the sample sheet.

**NOTE**
Reads that cannot be assigned to any sample are written to a FASTQ file for sample number 0, and excluded from downstream analysis.
• L001-The lane number.
• R1-The read. In this example, R1 means Read 1. For a paired-end run, there is at least one file with R2 in the file name for Read 2. When generated, index reads are I1 or I2.
• 001-The last segment is always 001.

**参考：**

https://support.illumina.com/help/BaseSpace_OLH_009008/Content/Source/Informatics/BS/NamingConvention_FASTQ-files-swBS.htm

\#####################################################################
\#版权所有 转载请告知 版权归作者所有 如有侵权 一经发现 必将追究其法律责任
\#Author: Jason
\#####################################################################