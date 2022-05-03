---
title: SpliceMap官网示例教程
tags:
  - RNA
url: archives/1043/index.html
id: 1043
categories:
  - Default Category
date: 2019-03-21 18:21:55
---

SpliceMap是一个从头开始发现和比对splice junction的工具。它提供高敏感度并且支持任意长度RNA-seq 序列片段read长度. SpliceMap将RNA-seq reads比对到参考基因组上用于发现splicing junctions. 它至少拥有与当前技术条件下其它分析工具同等的灵敏度和特异性。

官网	[http://web.stanford.edu/group/wonglab/SpliceMap/manual.html](http://web.stanford.edu/group/wonglab/SpliceMap/manual.html)

下载	[http://web.stanford.edu/group/wonglab/SpliceMap/download.html](http://web.stanford.edu/group/wonglab/SpliceMap/download.html)

示例教程	[https://web.stanford.edu/group/wonglab/SpliceMap/tutorial.html](https://web.stanford.edu/group/wonglab/SpliceMap/tutorial.html)

以官网SpliceMap 3.3.5.2 example (Linux-x86 64bit)为例，介绍如何用来自21号染色体的100k 条100bp的RNA reads寻找junction。

测试是否正常./bin/runSpliceMap，如果报错的话，需要到src文件夹运行 ./install.sh ../bin来安装SpliceMap，运行./install-bowtie.sh ../bin来安装

# 示例文件夹下面的结构

```
ls SpliceMap3352_example_linux-64
all.gene.refFlat.txt  bin  data  genome  INSTALL  LICENSE  output  run.cfg  src  temp
```




# run.cfg

最重要的文件，为文本文件，包含测序reads路径，基因组文件路径，配置设置等详见
https://web.stanford.edu/group/wonglab/SpliceMap/cfg.html，需要对每个数据集进行配置。在cfg文件中，注释以#开头，赋值用tag = value表示，比如genome_dir = ../../genome/hg18，多值用如下表示

```
> tag
value_1
value_2
...
<
```

# genome directory

该路径下包括物种的染色体，bowtie的索引，测试示例中仅放了21号染色体和相关bowtie的索引。

```
ls genome                                                      
chr21.1.ebwt  chr21.2.ebwt  chr21.3.ebwt  chr21.4.ebwt  chr21.fa  chr21.rev.1.ebwt  chr21.rev.2.ebwt
```


# data directory

样本的测序reads，真实使用中可以是其他位置。

# temp directory

在SpliceMap运行过程中的临时文件，最初的序列比对结果存储在这里，所以这个文件夹可能会很大。

# output directory

SpliceMap的输出结果文件夹。

# all.gene.refFlat.txt

包含来自ensembl，refseq，knowGene数据所有基因的注释，可以用来寻找新的junction。

# bin

SpliceMap的运行程序，不需要安装，可以拷贝到其他地方。

# src

包含SpliceMap/Bowtie源程序的文件夹。

# 运行SpliceMap

在example文件夹中，运行大概两到三分钟可以结束

<pre>./bin/runSpliceMap run.cfg</pre>

# 输出结果文件夹output

# junction_color.bed

包含发现的junctions，novel junction在bed文件中用红色表示，可以用UCSC基因组浏览器或cisGenome浏览器看。

```
track   name=junctions  description="SpliceMap junctions" itemRgb="On"
chr21   14669961        14672440        (2)[49_2](2/0)  50      -       14669961        14672440        96,96,96        2 50,50    0,2429
chr21   16125769        16127587        (1)[1_1](1/0)   50      +       16125769        16127587        192,192,192     2 50,50    0,1768
```

# junction_color.new.bed

不在all.gene.refFlat.txt文件中的新的junction。

```
track   name=junctions  description="SpliceMap junctions" itemRgb="On"
chr21   17186728        17208745        (2)[6_2](2/0)   50      +       17186728        17208745        255,0,0 2       50,50      0,21967
chr21   23658336        23666569        (1)[1_1](1/0)   50      -       23658336        23666569        255,192,192     2 50,50    0,8183
```

# junction_nUM_color.bed

junction_color.bed文件中的至少被一条唯一比对的read支持的junction。

```
track   name=junctions  description="SpliceMap junctions" itemRgb="On"
chr21   14669961        14672440        (2)[49_2](2/0)  50      -       14669961        14672440        96,96,96        2 50,50    0,2429
chr21   16125769        16127587        (1)[1_1](1/0)   50      +       16125769        16127587        192,192,192     2 50,50    0,1768
```

# junction_nUM_color.new.bed

在junction_nUM_color.bed中且不在all.gene.refFlat.txt中的junction。

```
track   name=junctions  description="SpliceMap junctions" itemRgb="On"
chr21   17186728        17208745        (2)[6_2](2/0)   50      +       17186728        17208745        255,0,0 2       50,50      0,21967
chr21   23658336        23666569        (1)[1_1](1/0)   50      -       23658336        23666569        255,192,192     2 50,50    0,8183
```

# coverage_up.wig

染色体位置中唯一比对的reads的覆盖度

```
track   type=bedGraph   name="SpliceMap unique coverage"
chr21   9944337 9944421 1
chr21   14070536        14070619        1
```

# coverage_down.wig

染色体位置中多重比对的reads的覆盖度

<pre>track   type=bedGraph   name="SpliceMap non-unique coverage"
chr21   16276385        16276484        -0.5
chr21   16277073        16277137        -0.5</pre>

# coverage_all.wig

所以比对上的reads在染色体上的覆盖度

<pre>track   type=bedGraph   name="SpliceMap all coverage"
chr21   9944337 9944421 1
chr21   14070536        14070619        1</pre>

# good_hits.sam

SAM格式存储的比对好的reads

```
R[87976]        73      chr21   9944337 255     85M     *       0       0       CATGTATCAACACCAAGTGCCATTTCTCTTAAGGATGCAAGGATGTTTTTTCCAAGATGGCAGATTACAGGCTTTTAGCATGCCT      IIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIII      NM:i:0  XC:i:15
R[28405]        177     chr21   14070536        255     100M    =       14070620        -15     GCAGAGGCTATTATTCATGGACTATCCAGTCTAACAGCTTGCCAGTTGAGAACGATATACATATGTCAGTTTTTGACAAGAATTTCAGCAGGAAAAACCC       IIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIII       MD:Z:40A43G15   NM:i:2  XC:i:0
R[28405]        113     chr21   14070620        255     100M    =       14070536        -15     GCAGCAGGAAAAACCCTTGATGCACAGTTTGAAAATGATGAACGAATTACACCCTTGGAATCAGCCCTGATGATTTGGGGTTCAATTGAAAAGGAACATG       IIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIII       MD:Z:42T42C14   NM:i:2  XC:i:0
```

# debug_logs

输出log

# 用自己的数据

重点修改cfg文件中genome_dir （参考基因组路径），reads_list1和2（fastq文件），annotations （基因注释文件），temp_path（中间数据存放路径），out_path（结果文件夹），bowtie_base_dir （bowtie2的index文件，如果没有，会在temp_path生成）

# 参考

https://web.stanford.edu/group/wonglab/SpliceMap/tutorial.html
大部分翻译这个tutorial，具体数据是自己跑tutorial得到的。

\#####################################################################
\#版权所有 转载请告知 版权归作者所有 如有侵权 一经发现 必将追究其法律责任
\#Author: Jason
\#####################################################################