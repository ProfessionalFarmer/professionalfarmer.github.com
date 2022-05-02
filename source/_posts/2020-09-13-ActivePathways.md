---
title: 整合多组学数据的通路富集分析-ActivePathways
tags:
  - Pathway
  - Enrichment
url: archives/1136.html
id: 1136
categories:
  - Default Category
date: 2020-09-13 01:03:23
---
我是在这篇文章（Integrative pathway enrichment analysis of multivariate omics data
）中遇到的合并多个p-value的操作。这篇文章是今年发表在NC上。所有的组学或者大规模的数据分析，都需要探索数据背后相关的生物学功能，所以通路富集分析非常普遍。通常的做法是基于单一组学、单一数据集的数据进行分析，随着生物学数据的爆发，大规模多组学数据变得普遍，这篇文章介绍了基于整合的多组学或多数据集的数据进行通路分析的工具ActivePathways。

![](/wp/f4w/2020/2020-09-12-ActivePathways-1.png)

# 方法
ActivePathways的方法，如下图：

(a) 需要的输入文件 

(1) 基于多组学数据集的基因P-value，传统的富集分析是单组学，只有一列，现在是多组学，对应多列P-value
(2) 基因集，这个和其他的通路富集分析一样，用来表示生物学过程和通路


(b) 

(1) 用Brown method合并基因的P-values，并且排序，用一个宽松的阈值来过滤检阳性的基因。
(2) 对每个通路，用排序的基因（从第一个开始从少到多作为sub-list）进行超几何检验，并找到最优的sub-list长度。
(3) 基因单一组学的数据进行富集分析，找到支持每个通路的证据。

(c) ActivePathways 提供整合之后的富集分析结果，相关的Brown P-value，支持通路的证据。还可以在Cytoscape中画Enrichmentmap的图，来分析更广泛的生物学主题。点为通路，边表示有共有基因。

![](/wp/f4w/2020/2020-09-12-ActivePathways-2.png)

# 例子

自然发到了NC这种水平的期刊上，出了豪华的团队外，ActivePathways一定有很厉害的功能才行。这篇文章提了好几个case study，我挑了一个，稍微讲一下，如下图。

昨天分析了乳腺癌中与预后相关的通路和过程，其中整合了三种数据集，TC（Tumor cell mRNA），TAC（Tumor adjacent cell mRNA）和CNA（拷贝数变异），这里也挺有意思，把TAC也纳入到P-values的矩阵中，并不是三个组学。

(a) Enrichment map，其中蓝色的表示仅由整合数据发现的通路，比如凋亡等，显示出其强大的功能。
(b) 乳腺癌Basel和HER2亚型中，与预后相关的免疫基因的Hazard Ratio（HR），显示出两种亚型间不同的免疫pattern。
(c) HER2亚型中，与预后相关的基因（凋亡过程负调控）在每个数据集上的P-value和整合后的Brown P-value。其中DUSP1在三个数据集中都非常显著，如果作者聚焦到了这个基因。
(d) 这个基因在肿瘤细胞mRNA，癌旁细胞mRNA和拷贝数变异三种数据集中，分成high和low两组，做生存分析，可以发现DUSP1低表达，预后显著好于高表达，以此证明ActivePathway的强大。

![](/wp/f4w/2020/2020-09-12-ActivePathways-3.png)

ActivePaths的下载地址：[https://github.com/reimandlab/ActivePathways](https://github.com/reimandlab/ActivePathways)。为一个R包，整理好P-values的数据框之后，一步命令即可分析，此外结果还可以在Cytoscape上用Enrichment map展示。

```
# scores是P-values的数据框,GMT是基因集
ActivePathways(scores, fname_GMT) 
```

# 参考

[https://www.nature.com/articles/s41467-019-13983-9](https://www.nature.com/articles/s41467-019-13983-9)

#####################################################################
#版权所有 转载请告知 版权归作者所有 如有侵权 一经发现 必将追究其法律责任
#Author: Jason
#####################################################################