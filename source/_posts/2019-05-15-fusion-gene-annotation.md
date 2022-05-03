---
title: Fusion Gene Annotation
tags:
  - Fusion
url: archives/1060/index.html
id: 1060
categories:
  - Default Category
date: 2019-05-15 09:45:45
---

STAR-FUSION和FusonAnnotator都属于Trinity Trinity Cancer Transcriptome Analysis Toolkit Fusion-finding modules。
CTAT_HumanFusionLib现阶段整合了各种资源帮助分析癌症生物学相关的fusion，同样也鉴别可能在正常样本只能出现的fusion。下载地址：https://data.broadinstitute.org/Trinity/CTAT_RESOURCE_LIB/

FusionAnnotator --genome_lib_dir GRCh37_gencode_v19_CTAT_lib_July192017/ctat_genome_lib_build_dir/ \
                   --annotate fusions.list.txt
fusions.list.txt为star-fusion的结果中的第一列，两个参与融合的基因中间用--连在一起，就可以用FusionAnnotator进行注释，相关的标签会注释到融合基因上。

会有三类标签，每类下面又有很多具体的来源标签：
Fusions relevant to cancer biology
Individual genes of cancer relevance, which may show up in fusions
Red Herrings: Fusion pairs that may not be relevant to cancer, and potential false positives.

通过注释，就可以了解到分析结果中的融合基因是否在其他数据库中出现过，或者可能是和癌症无关的突变。

参考：[https://github.com/FusionAnnotator/CTAT_HumanFusionLib/wiki](https://github.com/FusionAnnotator/CTAT_HumanFusionLib/wiki)