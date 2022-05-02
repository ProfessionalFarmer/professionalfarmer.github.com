---
title: Pacbio三代测序Primary Analysis Data文件夹
tags:
  - Pacbio
url: archives/1042.html
id: 1042
categories:
  - Default Category
date: 2019-03-20 18:08:34
---

三代测序很多年了，刚工作的时候在超算中心做过三代的拼接，没好好研究过之后就再也没接触过，现在要做三代的项目，从头学习，Primary Analysis Data为初步数据分析文件夹，类似下面的文件夹结构

```
/path/to/secondary/storage/2420294/0011
├── Analysis_Results
│   ├── m140415_143853_42175_c100635972550000001823121909121417_s1_p0.1.bax.h5
│   ├── m140415_143853_42175_c100635972550000001823121909121417_s1_p0.1.log
│   ├── m140415_143853_42175_c100635972550000001823121909121417_s1_p0.1.subreads.fasta
│   ├── m140415_143853_42175_c100635972550000001823121909121417_s1_p0.1.subreads.fastq
│   ├── m140415_143853_42175_c100635972550000001823121909121417_s1_p0.2.bax.h5
│   ├── m140415_143853_42175_c100635972550000001823121909121417_s1_p0.2.log
│   ├── m140415_143853_42175_c100635972550000001823121909121417_s1_p0.2.subreads.fasta
│   ├── m140415_143853_42175_c100635972550000001823121909121417_s1_p0.2.subreads.fastq
│   ├── m140415_143853_42175_c100635972550000001823121909121417_s1_p0.3.bax.h5
│   ├── m140415_143853_42175_c100635972550000001823121909121417_s1_p0.3.log
│   ├── m140415_143853_42175_c100635972550000001823121909121417_s1_p0.3.subreads.fasta
│   ├── m140415_143853_42175_c100635972550000001823121909121417_s1_p0.3.subreads.fastq
│   ├── m140415_143853_42175_c100635972550000001823121909121417_s1_p0.bas.h5
│   ├── m140415_143853_42175_c100635972550000001823121909121417_s1_p0.sts.csv
│   └── m140415_143853_42175_c100635972550000001823121909121417_s1_p0.sts.xml
├── m140415_143853_42175_c100635972550000001823121909121417_s1_p0.1.xfer.xml
├── m140415_143853_42175_c100635972550000001823121909121417_s1_p0.2.xfer.xml
├── m140415_143853_42175_c100635972550000001823121909121417_s1_p0.3.xfer.xml
├── m140415_143853_42175_c100635972550000001823121909121417_s1_p0.mcd.h5
└── m140415_143853_42175_c100635972550000001823121909121417_s1_p0.metadata.xml
```




**主要文件有**

# bas.h5文件和bax.h5文件

bas.h5和相关的bax.h5文件是PacBio@RS II初级分析（primary analysis）的主要输出文件，这些文件由设备产生到本地存储位置，作为后续SMRT分析软件进行alignment、consensus和variant分析的输入文件。
PacBio@RS II之前，单个bas.h5文件包含了所有测序数据，随着PacBio@RS II升级，通量和read长度都在增加，现在包含一个bas.h5和3个bax.h5文件（1-3.bax.h5）。bax.h5文件包含测序的base call的信息，bas.h5是三个bax.h5的重要指针。
用h5dupm -n [movie name].bas.h5命令看一下文件

```
FILE_CONTENTS {
 group      /
 group      /MultiPart
 dataset    /MultiPart/HoleLookup
 dataset    /MultiPart/Parts
 }
```



可以看到有一个MultiPart的group组，下面有两个数据集，一个是HoleLookup，一个是Parts。
/MultiPart/Parts提供相关对应的的三个bax.h5的文件名
/MultiPart/HoleLookup对应ZMW零模波导孔编号

单个的bax.h5文件结构和原来一致 ，有两个组，分别是PulseData和ScanData。ScanData
包含了用于测试的仪器信息，一般不会用到。PulseData下面重点看/PulseData/BaseCalls组
用命令h5dump -d /PulseData/BaseCalls/Basecall [movie name].bax.h5 ' head -10 查看数据集basecall如下序列

```
DATASET "/PulseData/BaseCalls/Basecall" {
   DATATYPE  H5T_STD_U8LE
   DATASPACE  SIMPLE { ( 305612594 ) / ( H5S_UNLIMITED ) }
   DATA {
   (0): 84, 84, 67, 84, 84, 67, 84, 84, 84, 84, 67, 71, 84, 71, 71, 84, 84,
   (17): 84, 84, 71, 84, 67, 84, 84, 84, 67, 84, 71, 84, 84, 84, 67, 84, 84,
   (34): 84, 67, 84, 84, 71, 84, 84, 67, 84, 71, 67, 71, 71, 84, 84, 84, 84,
   (51): 84, 84, 84, 84, 84, 84, 84, 84, 84, 84, 84, 84, 84, 84, 84, 84, 84,
   (68): 84, 84, 84, 84, 71, 84, 84, 71, 84, 84, 84, 84, 84, 84, 84, 84, 84,
```




其中A=> 65, C=> 67, G=>71, T=>84，与ASCII编码一致。

用h5dump -d /PulseData/BaseCalls/QualityValue bax.h5 ' head -10 查看数据集qualityvalue如下

```
DATASET "/PulseData/BaseCalls/QualityValue" {
   DATATYPE  H5T_STD_U8LE
   DATASPACE  SIMPLE { ( 305612594 ) / ( H5S_UNLIMITED ) }
   DATA {
   (0): 10, 11, 21, 12, 11, 9, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 14, 0, 0, 0, 10, 0, 1,
   (23): 0, 0, 15, 1, 1, 1, 0, 1, 1, 1, 1, 0, 2, 10, 0, 0, 0, 0, 0, 0, 14, 20, 1,
   (46): 1, 30, 1, 0, 0, 1, 22, 0, 19, 0, 1, 0, 0, 21, 1, 1, 1, 0, 0, 17, 0, 0, 1,
   (69): 1, 1, 30, 2, 1, 0, 2, 1, 0, 10, 0, 1, 1, 0, 1, 1, 13, 0, 0, 0, 1, 0, 0,
   (92): 1, 0, 5, 1, 0, 0, 1, 0, 2, 1, 0, 0, 21, 0, 1, 0, 0, 20, 0, 0, 0, 16, 1,
```




表示测错的概率，用的是phred socre，和Illumina类似。当然，我看的这个文件可以看出测序质量并不是很好。

具体的组和数据集的说明，可以参考：

[https://s3.amazonaws.com/files.pacb.com/software/instrument/2.0.0/bas.h5+Reference+Guide.pdf](https://s3.amazonaws.com/files.pacb.com/software/instrument/2.0.0/bas.h5+Reference+Guide.pdf)

# metadata.xml

包含测序仪ID，样本名，测序酶，试剂等元数据。
参考文件：[https://s3.amazonaws.com/files.pacb.com/software/instrument/2.0.0/Metadata+Output+Guide.pdf](https://s3.amazonaws.com/files.pacb.com/software/instrument/2.0.0/Metadata+Output+Guide.pdf)

# sts.xml

包含了单个movie的概括统计
参考文件：[https://s3.amazonaws.com/files.pacb.com/software/instrument/1.3.1/Statistics+Output+Guide.pdf](https://s3.amazonaws.com/files.pacb.com/software/instrument/1.3.1/Statistics+Output+Guide.pdf)

# 用h5dump查看pacbio数据

查看h5格式的文件可以用hdf5下的h5dump工具查看,安装如下

```
wget -c https://support.hdfgroup.org/ftp/HDF5/releases/hdf5-1.10/hdf5-1.10.5/src/hdf5-1.10.5.tar.gz
tar -xzvf hdf5-1.10.5.tar.gz
cd hdf5-1.10.5  
./configure &&make && make install
```




# 参考：

https://www.cnblogs.com/xudongliang/p/6908953.html
https://smrt-analysis.readthedocs.io/en/latest/Data-files-you-received-from-your-service-provider/

\#####################################################################
\#版权所有 转载请告知 版权归作者所有 如有侵权 一经发现 必将追究其法律责任
\#Author: Jason
\#####################################################################