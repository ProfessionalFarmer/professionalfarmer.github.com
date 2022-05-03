---
title: BCL文件与BCL2FAFSTQ程序简介
tags:
  - BCL
  - FASTQ
  - Illumina
url: archives/815/index.html
id: 815
categories:
  - Default Category
date: 2018-02-07 11:34:40
---

![](/wp/f4w/2020/2016-04-0301.jpg)

BCL文件
=====

测序产生的原始文件是BCL（binary base call）文件，测序仪在测序的时候，每个cycle都会测量编码不同颜色的通道强度，并确定最有可能的碱基类型。Real Time Analysis (RTA) 软件会将碱基类型和可信度（一个质量分数）。与FASTQ文件不同的是，BCL文件是实时产生，每个cycle的每个tile都会有一个对应文件，文件放在

`<run directory>/Data/Intensities/BaseCalls/L<lane>/C<cycle>.1`

文件的命名

 `s_<lane>_<tile>.bcl`

bcl2fastq
=========

该文件需要通过Illunima的软件或者第三方分析工具将BCL文件转成FASTQ文件。一般而言，数据下机之后，Illumina测序仪会自动将BCL转成FASTQ文件。有时候，根据实验需要，需要自己手工将BCL文件转成FASTQ文件，比如自己设计的index中含有简并碱基，或者需要调整一下转换的参数等。 Illumina提供bcl2fastq的程序包，共离线处理BCL文件，生成FASTQ文件。

```bash
bcl2fastq  -i /paht/to/run/Data/Intensities/BaseCalls/ \
       -o /output/dir --sample-sheet /paht/to/run/SampleSheet.csv \
       -R /paht/to/run/
```

bcl2fastq文件有很多参数可调，比如在FASTQ中记录read的index(fastq文件中会记录配对的index具体序列，以及会生成额外对应的index文件)，可以添加--create-fastq-for-index-reads选项。 如果允许index有mismatch的话，可以通过--barcode-mismatches设置。 --fastq-compression-level可以设置生成的FASTQ.GZ文件的压缩比例 安装如下

```bash
unzip bcl2fastq2-v2.17.1.14.tar.zip
tar -xvzf bcl2fastq2-v2.17.1.14.tar.gz
./bcl2fastq/src/configure --prefix=/path/to/install/
make
make install
```

安装过程中，如果遇到一下问题，请更新gcc版本 问题1 cc1plus: error: unrecognized command line option "-std=c++11" 问题2 undefined reference to `boost::re\_detail::perl\_matcher collect2: error: ld returned 1 exit status 软件选项说明如下：

```java
BCL to FASTQ file converter
bcl2fastq v2.17.1.14
Copyright (c) 2007-2015 Illumina, Inc.

Command-line options:
  -h [ --help ]                                     produce help message and exit
  -v [ --version ]                                print program version information
  -l [ --min-log-level ] arg (=INFO)              minimum log level
                                                          recognized values: NONE, FATAL, ERROR, WARNING, INFO, DEBUG, TRACE
  -i [ --input-dir ] arg (=<runfolder-dir>/Data/Intensities/BaseCalls/)
                                                          path to input directory
  -R [ --runfolder-dir ] arg (=./)         path to runfolder directory
  --intensities-dir arg (=<input-dir>/../)        path to intensities directory
                                                          if intensities directory is specified, also input directory must be specified
  -o [ --output-dir ] arg (=<input-dir>)                path to demultiplexed output
  --interop-dir arg (=<runfolder-dir>/InterOp/)   path to demultiplexing statistics directory
  --stats-dir arg (=<output-dir>/Stats/)                path to human-readable demultiplexing statistics directory
  --reports-dir arg (=<output-dir>/Reports/)       path to reporting directory
  --sample-sheet arg (=<runfolder-dir>/SampleSheet.csv)
                                                                              path to the sample sheet
  --aggregated-tiles arg (=AUTO)                  tiles aggregation flag determining structure of input files
                                                   recognized values:
                                                      AUTO Try to detect correct setting
                                                      YES  Tiles are aggregated into single input file
                                                      NO   There are separate input files for individual tiles
                                                  
  -r [ --loading-threads ] arg (=4)               number of threads used for loading BCL data
  -d [ --demultiplexing-threads ] arg          number of threads used for demultiplexing
  -p [ --processing-threads ] arg                 number of threads used for processing demultiplexed data
  -w [ --writing-threads ] arg (=4)               number of threads used for writing FASTQ data
                                                                    this must not be higher than number of samples
  --tiles arg                                 Comma-separated list of regular expressions to select only a subset of the tiles 
                                                  available in the flow-cell. Multiple entries allowed, each applies to the corresponding base-calls.
                                                  For example:
                                                   * to select all the tiles ending with '5' in all lanes:
                                                       --tiles [0-9][0-9][0-9]5
                                                   * to select tile 2 in lane 1 and all the tiles in the other lanes:
                                                       --tiles s_1_0002,s_[2-8]
  --minimum-trimmed-read-length arg (=35)         minimum read length after adapter trimming
  --use-bases-mask arg                                             Specifies how to use each cycle.
  --mask-short-adapter-reads arg (=22)            smallest number of remaining bases (after masking bases below the minimum 
                                                                           trimmed read  length) below which whole read is masked
  --adapter-stringency arg (=0.9)                  adapter stringency
  --ignore-missing-bcls                                 assume 'N'/'#' for missing calls
  --ignore-missing-filter                                assume 'true' for missing filters
  --ignore-missing-positions                         assume \[0,i\] for missing positions, where i is incremented starting from 0
  --ignore-missing-controls                           assume 0 for missing controls
  --write-fastq-reverse-complement              Generate FASTQs containing reverse complements of actual data
  --with-failed-reads                                        include non-PF clusters
  --create-fastq-for-index-reads                     create FASTQ files also for index reads
  --find-adapters-with-sliding-window           find adapters with simple sliding window algorithm
  --no-bgzf-compression                                Turn off BGZF compression for FASTQ files
  --fastq-compression-level arg (=4)              Zlib compression level (1-9) used for FASTQ files
  --barcode-mismatches arg (=1)                   number of allowed mismatches per index
                                                                        multiple entries, comma delimited entries, allowed; each entry is applied to the 
                                                                        corresponding index;last entry applies to all remaining indices
  --no-lane-splitting                             Do not split fastq files by lane.
```

软件地址 http://support.illumina.com.cn/downloads/bcl2fastq-conversion-software-v217.html 

文档手册 http://support.illumina.com/content/dam/illumina-support/documents/documentation/software\_documentation/bcl2fastq/bcl2fastq\_letterbooklet_15038058brpmi.pdf

\##################################################################### #版权所有 转载请告知 版权归作者所有 如有侵权 一经发现 必将追究其法律责任 
\#Author: Jason
\#####################################################################