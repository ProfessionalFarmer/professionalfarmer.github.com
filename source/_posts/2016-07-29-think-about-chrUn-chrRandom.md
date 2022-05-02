---
title: 思考--在比对时，关于是否将chr*_random和chrUn_*序列放在参考基因组中的思考
tags:
  - Align
  - Genome
  - Viewpoint
url: archives/764.html
id: 764
categories:
  - Default Category
date: 2016-07-29 15:45:34
---

通常认为chr1-22，chrY，chrX和chrM为参考基因组序列，于是包括我在内的很多人，分别下载了25条染色体序列，合并成一个fasta文件，用bowtie2或者BWA构建index，用于下一步的read比对，然后是各种分析（包括突变、转录表达等）。

UCSC下载的HG19版本的整个参考基因组文件**http://hgdownload.cse.ucsc.edu/goldenPath/hg19/bigZips/chromFa.tar.gz**中，除还包括chr*_random和chrUn_*序列（暂时理解为补丁序列，真实的补丁序列称呼常见assemble过程，见[**http://www.ncbi.nlm.nih.gov/projects/genome/assembly/grc/info/patches.shtml**](http://www.ncbi.nlm.nih.gov/projects/genome/assembly/grc/info/patches.shtml)，有fix 和novel patch，这里我们现在只讨论chr*_random和chrUn_*）。

The **chr*_random** sequences are unplaced sequence on those reference
chromosomes.

The **chrUn_*** sequences are unlocalized sequences where the corresponding
reference chromosome has not been determined.

当然如果DNA或RNA测序的read比对到chr*_random 和 chrUn_* 序列上，显示大多数人都不关注这些序列上信息，我想这也是很多人不把chr*_random 和 chrUn_* 放到参考基因组fasta文件中的原因。但是，chr*_random 和 chrUn_* 显然是存在的，只不过现在暂时没有确定位置或者后续用于基因组序列更正。

如果参考基因组序列中不包含chr*_random 和 chrUn_*序列，那么原来属于chr*_random 和 chrUn_*的read则有可能比对到（不是一定）chr1-22，chrX，chrY上的相似区域（这些区域与chr*_random 和 chrUn_*中的部分区域相似），造成假阳性比对，后续这些reads提供的信息都是不可靠的。

如果参考基因组序列中包含chr*_random 和 chrUn_*序列，那么来自这些区域的reads则会正确的比对到这个地方，没有假阳性比对，只不过后续分析不需要考虑chr*_random 和 chrUn_*即可。

```
假设有一条read来自chr1_random，
条件                                     比对结果             分析结果
基因组fa文件包含chr1_random序列          比对到chr1_random    后续不考虑
基因组fa文件中不包含chr1_random序列      比对到chr1           造成假阳性<
```


举个例子，以前，我们确认一个突变是否存在，看覆盖这个点的read上有多少突变的碱基，如果覆盖这个点的read本来属于chr*_random 和 chrUn_*序列的，但比对到这个地方，即使这个位点的突变碱基再多，也是个假阳性突变，影响后续分析。

**综上，参考基因组需要放chr*_random和chrUn_*序列，降低reads比对时的假阳性。**

\#####################################################################
\#版权所有 转载请告知 版权归作者所有 如有侵权 一经发现 必将追究其法律责任
\#Author: Jason
\####################################################################