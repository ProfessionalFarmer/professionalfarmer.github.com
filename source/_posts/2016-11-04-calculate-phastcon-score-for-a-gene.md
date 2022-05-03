---
title: Calculate phastCon Score for a gene ---- 计算基因的phastCon平均分，判断基因保守型
tags:
  - bedops
  - BEDtools
  - phastCon
url: archives/788/index.html
id: 788
categories:
  - Default Category
date: 2016-11-04 21:45:25
---


Calculate phastCon Score for a gene ---- 计算基因的phastCon平均分，判断基因保守型

PhastCon socre is the score from 0 to 1 to show the conservation level.

A score showing the posterior probability that phastCons's phylogenetic hidden Markov model (HMM) is in its most conserved state at that base position.

The phastCons scores represent probabilities of negative selection and range between 0 and 1. 

Short highly-conserved regions and long moderately conserved regions can both obtain high scores. 

也就是说如果某个位点或者一段序列的phastCon分值高的话，表示保守型较高。

# 1，下载phast score的wigFix格式文件（以19号染色体为测试）

```
wget -c http://hgdownload.cse.ucsc.edu/goldenPath/hg19/phastCons46way/placentalMammals/chr19.phastCons46way.placental.wigFix.gz
gunzip -k chr19.phastCons46way.placental.wigFix.gz

head chr19.phastCons46way.placental.wigFix

fixedStep chrom=chr19 start=60001 step=1
0.412
0.407
0.394
0.393
0.381
0.381
0.369
0.345
0.291
```

wigFix格式是 fixed 的 Wiggle 格式，根据上面的前几行，应该能够看出该文件表示19号染色体，从60001位置开始，每一步step（base）的phastCon分值。

# 利用bedops，将wig转成bed文件

bedops的官网 [https://bedops.readthedocs.io/en/latest/](https://bedops.readthedocs.io/en/latest/) ， 转成bed文件便于利用bed工具进行处理。

```
wig2bed chr19.phastCons46way.placental.wigFix > chr19.phastCons46way.placental.bed
```

如果需要合并的话，运行下面的命令即可，这里以chr19染色体为例，就不合并了。
bedops --everything chr*.bed > vertebrate.phastCons46.bed

# 将gtf文件分割成已基因为单位的gtf文件

gtf文件中只有chr19染色体的基因注释信息。

```
mkdir test
awk -F 't' '{split($9,a,";"); split(a[1],a," "); gsub(""", "", a[2]); x="test/"a[2]".gtf"; print >> ("test/"a[2]".gtf"); close(x);}' Homo_sapiens.GRCh38.85.gtf && rm test/.gtf
```




# 将gft文件转成bed文件

```
rm test/*bed
for fn in `ls test/*gtf`; do
    gene=`echo $fn ' cut -d . -f 1`
    gtf2bed $fn ' sort -k1,1 -k2,2n >> $gene.bed
    rm $fn
done
```


gtf2bed是[前面文章](http://wp.zxzyl.com/?p=270)中提到的，只要能将gtf转成bed就可。

# 利用bedtools工具计算每个序列的平均phastCon score

```
# 最新版的bedtools有split选项
for fn in `ls test/*.bed`;do
bedtools map -split -sorted -a $fn -b chr19.phastCons46way.placental.bed -o mean ' awk -F 't' '{printf ("%st%4fn", $1,$NF)}'
done
```


bedtools官网 [bedtools.readthedocs.io](http://bedtools.readthedocs.io) ，mean表示计算平均分。结果如下，平均分越高越保守。

```
chr19   531711  542092  ENST00000215574 0.388707
chr19   531768  536715  ENST00000586788 0.317417
chr19   532031  542092  ENST00000586283 0.431241
chr19   532099  541585  ENST00000607527 0.643244
chr19   535836  542087  ENST00000606065 0.404337
chr19   536952  542042  ENST00000606400 0.288264
chr19   541216  541661  ENST00000593036 0.434159
chr19   489175  505342  ENST00000587541 0.032945
chr19   496453  505207  ENST00000613880 0.186624
chr19   496453  505207  ENST00000617201 0.194969<
```




# 参考：

**https://www.biostars.org/p/150152/**

**http://ccg.vital-it.ch/mga/mm9/phastcons/phastcons.html**

\#####################################################################
\#版权所有 转载请告知 版权归作者所有 如有侵权 一经发现 必将追究其法律责任
\#Author: Jason
\########################################################################################################################################