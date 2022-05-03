---
title: AMY-Tree分析Y染色体 ---分类树
tags:
  - AMY-Tree
  - 'Y'
url: archives/763/index.html
id: 763
categories:
  - Default Category
date: 2016-07-22 16:31:16
---

AMY-Tree下载地址
============

[https://bio.kuleuven.be/eeb/lbeg/software](https://bio.kuleuven.be/eeb/lbeg/software) 解压下载的压缩文件

AMY-Tree输入文件
============

输入文件的格式要求在解压出来的 Manual （**_AMY-tree v2.0 User Manual.pdf_**）里可以看到

1\. Y-SNP (or SNP calling data) file
------------------------------------

假设我们手里有VCF文件，那么提取VCF文件中的chrY中的位点即可，但是符合AMY-Tree的格式要求。

`cat sample.vcf | grep -Ev "^#" | grep "chrY" | awk '{print $1"t"$2"t"$4"t"$5"t"$3}' |  sed "s#.#x#g" > chrY.convert`

2\. Phylogenetic tree file
--------------------------

对应解压出来的 UpdatedTree_v2.1.txt 文件

3\. Mutation conversion file
----------------------------

对应解压出来的 MutationConversion_v2.1.txt

4，Hg18/Hg19 Y-chromosome fasta file
-----------------------------------

可以从UCSC中下载 http://hgdownload.soe.ucsc.edu/goldenPath/hg19/chromosomes/chrY.fa.gz

5，Status file of Hg18/Hg19 Y-chromosome
---------------------------------------

生成第一个输入文件的status文件，需要用到解压出来的getStatusReference.pl脚本

`perl getStatusReference.pl chrY.fa chrY.convert hg19 status.Y.txt`

6，Quality control file
----------------------

对应解压出来的 qualityControl_v2.0.txt

7，Version (hg18 or hg19)
------------------------

基因组版本，我用的是hg19

运行命令：
=====

`perl AMY-tree\_v2.0.pl ./chrY.convert  ./test/ ./UpdatedTree\_v2.1.txt  ./MutationConversion\_v2.1.txt ./chrY.fa ./status.Y.txt ./qualityControl\_v2.0.txt hg19
`

./test是输出文件路径

输出结果
====

结果文件夹中有

    chrY.con\_analysis.txt     chrY.con\_newSNPs.txt  chrY.con_statusSNPs.txt  chrY.convert
    chrY.con\_ConvNotTree.txt  chrY.con\_quality.txt  chrY.con_status.txt      status.Y.txt

其中chrY.con_analysis.txt中的内容为 

    QUALITY 
    ------- 
    F: not R & not G 
    0.866666666666667 (insufficient) 
    
    VERTICAL 
    -------- 
    $ O2a2c2c* \[O-Page23*\] 
    $ Root* \[Root\] 
    
    HORIZONTAL ---------- 
    ! Root COMBI ----- 
    % O2a2c2c* \[O-Page23*\] 
    % Root* \[Root\] 
    
    SPECIFIC -------- 
    @ O2a2c2c* \[O-Page23*\] 
    
    RESULTS 
    ------- 
    > O2a2c2c* \[O-Page23*\] 

结果为**O2a2c2c** 
下面的内容来自https://github.com/fjkfwz/AMY-Tree，感谢作者 

AMY算法可以对确定Y染色体单倍群提供准确的意见，已经通过来自不同地区的109个男性的全基因组数据来成功的验证AMY树的准确度，AMY树搜索算法使用Y染色体单倍群树，并且可以查找步骤拆分为各个子算法来并行的加快程序的处理速度，通过判断每个节点的状态来确定样品所在的染色体单倍群，AMY树的算法如下： 

（1）垂直子算法，垂直子算法能够通过检查每个叶节点的Y染色体单倍型对应的SNP位点的状态是否为真，由于这棵树所有的根节点都在左边而所有的叶节点都在右边，因此这个子算法又被称之为垂直子算法，在图中的矩形，方框中的单倍型为真，X1a，Z2b* and Z2b3， （

2）但是垂直子算法并只检查了每棵树的叶节点，没有深入到树的内部，因此不能够排除SNP位点存在假阳性的可能，从而返回了一个错误的结果，因此需要对从根出发一直到每个叶节点通过节点间的链接的水平子算法来计算，由于该算法大致上是从左到右水平判断每个节点的状态，因此这个子算法也被称之为水平子算法，这种算法从左边的根节点开始逐个的检查每个子节点的状态是否为真，知道没有节点没有其子节点或者改节点的所有子节点的状态均为否，并且返回最后一个节点的状态为True的节点，如上图水平算法返回的结果为Z2b， （

3）接下来需要中和垂直子算法和水平子算法的结果来获取更准确的判断结果，只有当垂直算法返回的叶节点同时该节点也存在于水平子算法的结果中将会直接有第三子算法返回分类的结果，但是这个算法同样会由于在水平算法中纯在假阴性的节点从而照成结果的误判，如图在垂直子算法返回了结果为X1a，Z2b* and Z2b3，水平子算法返回的结果为Z2b，由于Z1的点与水平子算法的结果Z2b并不相符，因此只保留 Z2b* and Z2b3a两个点，保留的两个点均为Z2b的子节点因此，由于SNP Calling不可避免的存在大量的误差因此，因此返回保留的两个结果。 

（4）第四个子算法继续对子树经行判断，查找匹配链条最为完整的路径的叶节点并返回查找/结果，本例中，该步骤返回的结果为Z2b3a，如果存在多个匹配的结果这返回匹配结果的列表作为Amy树查找的结果。 AMY树算法的强大之处在于可以组合各种不同的策略充分的利用SNP calling的结果，从而降低由于SNP Calling或者是Y染色体单倍型树造成的负面影响。

参考：
===

AMY-tree v2.0 User Manual.pdf [https://github.com/fjkfwz/AMY-Tree](https://github.com/fjkfwz/AMY-Tree) 

[https://bio.kuleuven.be/eeb/lbeg/software](https://bio.kuleuven.be/eeb/lbeg/software) 

[http://isogg.org/tree/index.html](http://isogg.org/tree/index.html) 

\#####################################################################
\#版权所有 转载请告知 版权归作者所有 如有侵权 一经发现 必将追究其法律责任
\#Author: Jason
\####################################################################