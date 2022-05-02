---
title: RNA测序到底可不可靠？(转)
tags:
  - Sequencing
url: archives/701.html
id: 701
categories:
  - Default Category
date: 2014-09-15 19:20:19
---

RNA测序可以检测人类和其他生物的基因表达情况。最近这一方法在生物科学和医学研究中非常流行，而且正在逐渐走向临床应用。与之前的方法相比，RNA测序的优势是便于研究选择性剪切形成的基因异构体或转录本。

那么RNA测序到底可不可靠呢？日前，由美国FDA牵头的测序质量控制(SEQC)项目对RNA测序的准确性、可重现性和信息含量进行了综合性评估，并将初步调查结果发表在近日的Nature Biotechnology杂志上。

研究团队使用RNA参照样本，在全球多个实验室的Illumina HiSeq、Life Technologies SOLiD、Roche 454平台上进行了检测。(深圳华大基因、复旦大学、华东师范大学等单位参与了这一项目。)研究人员主要是评估RNA测序在接头区域和差异性表达谱中的表现，并将其与芯片和定量PCR(qPCR)进行比较。

研究人员发现，所有测序深度都会出现未注释的外显子-外显子连接区域，其中80%以上都得到了qPCR的验证。用RNA测序检测相对表达可以得到准确且可重复的结果，但RNA测序和芯片都不能提供精确的绝对测量，而且研究用到的平台都存在基因特异性的偏好，包括qPCR。

数据分析的算法也会对RNA测序产生很大影响，不同算法生成的转录本数据差异很大。研究显示，赫尔辛基大学和曼彻斯特大学开发的BitSeq能生成最可靠的结果，这一方法以概率建模为基础。

这项研究获得的完整SEQC数据集拥有超过10Tb读取，为评估RNA测序分析提供了宝贵的资源。

转自 http://www.biodiscover.com/news/research/112652.html

原文original paper: http://www.nature.com/nbt/journal/v32/n9/full/nbt.2957.html

We present primary results from the Sequencing Quality Control (SEQC) project, coordinated by the US Food and Drug Administration. Examining Illumina HiSeq, Life Technologies SOLiD and Roche 454 platforms at multiple laboratory sites using reference RNA samples with built-in controls, we assess RNA sequencing (RNA-seq) performance for junction discovery and differential expression profiling and compare it to microarray and quantitative PCR (qPCR) data using complementary metrics. At all sequencing depths, we discover unannotated exon-exon junctions, with >80% validated by qPCR. We find that measurements of relative expression are accurate and reproducible across sites and platforms if specific filters are used. In contrast, RNA-seq and microarrays do not provide accurate absolute measurements, and gene-specific biases are observed for all examined platforms, including qPCR. Measurement performance depends on the platform and data analysis pipeline, and variation is large for transcript-level profiling. The complete SEQC data sets, comprising >100 billion reads (10Tb), provide unique resources for evaluating RNA-seq analyses for clinical and regulatory settings.