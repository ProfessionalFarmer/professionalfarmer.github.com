---
title: BreakDancer检测结构突变SV实战
tags:
  - Sequencing
  - SV
url: archives/720.html
id: 720
categories:
  - Default Category
date: 2016-01-09 01:26:21
---

一，介绍
----

BreakDancer包含两个互补的程序：BreakDancerMax和BreakDancerMini。

BreakDancerMax根据二代测序read比对时，出现的异常比对，预测插入，缺失，倒位，染色体间或染色体内易位等五种结构突变。 

BreakDancerMini则侧重于检测small indel。新版本的breakdancer已经不在包含BreakDancerMini，作者推荐使用**Pindel**检测small indels (10-80 bp)。

项目地址：[https://github.com/genome/breakdancer](https://github.com/genome/breakdancer "https://github.com/genome/breakdancer") [http://breakdancer.sourceforge.net/](http://breakdancer.sourceforge.net/ "http://breakdancer.sourceforge.net/")

二，安装
----

BreakDancer利用跨平台编译工具cmake进行编译,如果没有安装cmake，要先安装cmake 
`$ sudo apt-get install cmake`

git clone BreakDancer项目到本地，--recursive要添加，因为添加这个参数之后，BreakDancer引用的其他模块才会一并克隆到本地。modules说明在.gitmodules文件中。 

`$ git clone --recursive https://github.com/genome/breakdancer.git` 

创建build文件夹，并进入

    $ cd breakdancer 
    $ mkdir build 
    $ cd build

执行cmake命令，指定编译发行版，并制定安装路径

`$ cmake .. -DCMAKE_BUILD_TYPE=release -DCMAKE_INSTALL_PREFIX=/usr/local` 

编译 

    $ make 
    $ sudo make install

有些教程提到要将samtools的路径添加到系统变量中，即在~/.profile或者~./bashrc中export PATH="${PATH}:/path/to/samtools。因为本人的服务器samtools本来就在环境变量中，所以没有设置，我在后续运行过程中发现breakdancer会调用samtools，所以请确保samtools在环境变量中。

在/path/tp/breakdancer/build/bin的目录下，会看到breakdancer-max。运行下试试，是不是正确输出了用法啦。

```bash
$ ./breakdancer-max

breakdancer-max version 1.4.5-unstable-66-4e44b43 (commit 4e44b43)

Usage: breakdancer-max

Options:
-o STRING operate on a single chromosome [all chromosome]
-s INT minimum length of a region [7]
-c INT cutoff in unit of standard deviation [3]
-m INT maximum SV size [1000000000]
-q INT minimum alternative mapping quality [35]
-r INT minimum number of read pairs required to establish a connection [2]
-x INT maximum threshold of haploid sequence coverage for regions to be ignored [1000]
-b INT buffer size for building connection [100]
-t only detect transchromosomal rearrangement, by default off
-d STRING prefix of fastq files that SV supporting reads will be saved by library
-g STRING dump SVs and supporting reads in BED format for GBrowse
-l analyze Illumina long insert (mate-pair) library
-a print out copy number and support reads per library rather than per bam, by default off
-h print out Allele Frequency column, by default off
-y INT output score filter [30]
```



三，新功能介绍
-------

-a 指定根据library检测copy number而不是根据每个bam文件

-h 打印碱基频率，因为相比于DEL，碱基频率更加准确 

-y int指定输出SV call的phred score 

breakdancer直接利用perl版本的samtools，但是bam文件中一定要包含 readgroup (@RG) tag

四，运行
----

BreakDancerMax接受MAQ, BWA, NovoAlign and Bfast等比对软件的比对输出文件。此外还有一个以tab分割的配置文件，指定比对文件的位置，检测参数和样本信息。如果比对结果文件是sam/bam格式，可以利用bam2cfg.pl脚本自动生成配置文件（相信现在的比对结果文件都是BAM或者SAM文件）。bam2cfg.pl依赖AlnParser.pm。如果一个bam文件中包含多个library的reads，请一定正确指定readgroup。picard可以后续添加readgroup，samtools可以。不过还是建议在比对的时候就指定这些信息。

### 配置bam2cfg.pl所依赖的包

bam2cfg.pl在/path/to/breakdancer/perl/中,但是在运行bam2cfg.pl时报错： 

还有其他各种各样的错，比如安装GD时，提示我'YAML' not installed，安装yaml提示我 libyaml-cpp0.3-dev : Conflicts: libyaml-cpp-dev but 0.5.1-1 is to be installed E: Unable to correct problems, you have held broken packages. 还提示我Could not find gdlib-config in the search path. Please install libgd 2.0.28 or higher. Warning: ExtUtils::CBuilder not installed or no compiler detected Has already been unwrapped into directory .cpan/build/GD-2.56-hyKkKj '/usr/bin/perl Build.PL --installdirs site' returned status 512, won't make等等 

解决办法，下面按顺序包含了解决我运行bam2cfg.pl时遇到问题的命令：

```bash
$ sudo apt-get install aptitude
$ sudo aptitude install yaml* #解决 install YAML # 'YAML' not installed libyaml-cpp0.3-dev : Conflicts: libyaml-cpp-dev but 0.5.1-1 is to be installed E: Unable to correct problems, you have held broken packages.


$ wget https://github.com/libgd/libgd/releases/download/gd-2.1.1/libgd-2.1.1.tar.gz -P ./
$ tar -xvzf libgd-2.1.1.tar.gz
$ cd libgd-2.1.1
$ ./configure
$ make
$ sudo make install


$ sudo apt-get -y install libgd2-xpm-dev build-essential #Could not find gdlib-config in the
$ search path. Please install libgd 2.0.28 or higher.


#install GD
#解决Checking for stray libgd header files...none found.
$ wget http://search.cpan.org/CPAN/authors/id/L/LD/LDS/GD-2.53.tar.gz -P ./
$ tar -xvzf GD-2.53.tar.gz
$ cd GD-2.53
$ perl Makefile.PL
$ make
$ make install
$ cd ../


#install dependency
#need sudo，解决依赖
$ sudo cpan install ExtUtils::CBuilder
$ sudo cpan install YAML
$ sudo cpan install GD::Text
$ sudo cpan install GD::Graph
$ sudo cpan install GD::Graph::histogram
```

其实，我前面的文章中就提到过安装GD module，而且也把脚本和模块打包了，不过当时我是找的别人的脚本，想知道在哪吗，[自己去找](http://wp.zxzyl.com/?p=81 "自己去找")（来打我呀）。今天心血来潮非要想自己解决，折腾了一天。亲，我告诉你，一定要先安装libgd，别问我为什么，妹的，我一层一层解决问题，最终发现先安装libgd就可以了（cry）。

此时运行bam2cfg.pl会显示

```bash
Usage: bam2cfg.pl
Options:
-q  INT Minimum mapping quality \[35\]
-m  Using mapping quality instead of alternative mapping quality
-s  Minimal mean insert size \[50\]
-C  Change default system from Illumina to SOLiD
-c  FLOAT Cutoff in unit of standard deviation \[4\]
-n  INT Number of observation required to estimate mean and s.d. insert size \[10000\]
-v  FLOAT Cutoff on coefficients of variation \[1\]
-f  STRING A two column tab-delimited text file (RG, LIB) specify the RG=>LIB mapping, useful when BAM header is incomplete
-b  INT Number of bins in the histogram \[50\]
-g  Output mapping flag distribution
-h  Plot insert size histogram for each BAM library
```

### 运行bam2cfg.pl生成配置文件

    $ cd /path/to/data 
    $ perl /path/to/breakdancer/perl/bam2cfg.pl ./your.bam

若报错：

Coefficient of variation *** in library *** is larger than the cutoff 1, poor quality data, excluding from further analysis. 

则添加-v 参数，即`perl /path/to/breakdancer/perl/bam2cfg.pl -v float ./your.bam` 

输出如下 
\[Sat Jan 9 00:11:50 2016 ../software/breakdancer/perl/bam2cfg.pl\] Processing bam: ZZ3.sort.bam 
\[Sat Jan 9 00:11:52 2016 ../software/breakdancer/perl/bam2cfg.pl\] selected\_libs is : 1 \[Sat Jan 9 00:11:52 2016 ../software/breakdancer/perl/bam2cfg.pl\] Closing BAM file 
\[Sat Jan 9 00:11:52 2016 ../software/breakdancer/perl/bam2cfg.pl\] Send TERM signal for 17060 
\[Sat Jan 9 00:11:54 2016 ../software/breakdancer/perl/bam2cfg.pl\] samtools pid process 17060 is still there... 
\[Sat Jan 9 00:11:54 2016 ../software/breakdancer/perl/bam2cfg.pl\] invoking kill -9 on 17060 ... 
\[Sat Jan 9 00:11:54 2016 ../software/breakdancer/perl/bam2cfg.pl\] Closing samtools process : 17060 
readgroup:N63\_S1 platform:ILLUMINA map:your.bam readlen:95.56 lib:N63_S1 num:9994 lower:0.00 upper:747397.59 mean:458.80 std:8964.47 SWnormality:minus infinity exe:samtools view 

在termianl里面就会看到最后两行，正是 bam2cfg.pl生成的配置文件的内容，我们要将这两行重定向到文件your.bam.cfg中：

`$ perl /path/to/breakdancer/perl/bam2cfg.pl -v float ./your.bam > your.bam.cfg` 

悄悄的告诉你，不要担心前几行会被重定向到文件中，因为前几行诗错误输出，后两行才是标准输出，只有后两行会被重定向到文件中。 运行breakdancer-max 检测结构突变

    $ cd /path/to/data
    $ /path/to/breakdancer/build/bin/breakdancer-max your.bam.cfg

输出文件格式： 

\#Chr1 Pos1 Orientation1 Chr2 Pos2 Orientation2 Type Size Score num\_Reads num\_Reads_lib ZZ3.sort.bam
chr1 762050 367+5- chr1 762176 367+5- ITX -368 50 5 your.bam|5 NA chr1 976553 217+7- 
chr1 976928 217+7- ITX -374 40 7 your.bam|7 NA 
chr1 946728 7+0- chr1 1256543 105+0- INV 309173 61 2 your.bam|2 10.05 

1-3列和4-6列被用来指定两个SV断点的坐标。一列为染色体chr，一列为位置pos，一列为方向orientation，正负号代表reads比对到anchoring区域的方向，数字代表比对到这个位置的reads数目。 

第7列表示SV的类型，分别有： DEL (deletions), INS (insertion), INV (inversion), ITX (intra-chromosomal translocation), CTX (inter-chromosomal translocation), and Unknown. 

第8列表示SV的大小，可以忽略正负号的意义，对染色体间易位无用。 

第9列可信度得分。 

第10列支持该SV的reads数目。 

第11列，library中支持该SV的reads数目 第12列run parameter Ref：https://github.com/genome/breakdancer

\##################################################################### 
\#版权所有 转载请告知 版权归作者所有 如有侵权 一经发现 必将追究其法律责任 
\#Author: Jason
\#####################################################################