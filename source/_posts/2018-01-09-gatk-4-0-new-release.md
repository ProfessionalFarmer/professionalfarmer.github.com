---
title: 2018-01-09 GATK 4.0 正式发布
tags:
  - GATK
  - Variant
url: archives/854.html
id: 854
categories:
  - Default Category
date: 2018-01-20 20:46:55
---

![hhttps://theme.zdassets.com/theme_assets/2378360/df085f154321faac9159dda57f50103b87a4f743.png](https://theme.zdassets.com/theme_assets/2378360/df085f154321faac9159dda57f50103b87a4f743.png) 

GATK4正式版已经发布，快去体验啦。GATK4在上一年提出开源，并放出beta版本，现在终于姗姗来迟。

GATK4是业界第一次涵盖了胚细胞和体细胞基因型分析中的主要突变类型的基因组分析工具，且已经开源。新版本的GATK为了解决性能瓶颈近乎完全重构，提高了速度和扩展性有不失其过往的准确度。

GATK4包含了备受大家喜爱的pipeline和新工具，汲取了机器学习和神经网络算法的优点。

GATK早期版本关注检测胚细胞短突变（germline short variant），新版本将体细胞短突变（somatic short variant）检测工具Mutect2也整合在内，Mutect2整合广泛使用的算法Mutect和GATK卓越的胚细胞突变检测算法HaplotypeCaller。除了短突变检测外，GATK4增加了检测胚细胞和体细胞拷贝数变异的流程，增加了基于体细胞等位拷贝数（somatic allelic CNV (ACNV)）的肿瘤异质性评估。这些流程经过重构，无缝用于gene panel、外显子到全基因组的测序数据。

GATK4同时包含了早期可以使用现在依然在开发的结构变异（structural variant）检测，胚细胞拷贝数变异CNV检测使用了机器学习的方法，基于卷积神经网络（Convolutional Neural Networks，CNN）的胚细胞短突变过滤方法。

GATK4对性能、灵活性、速度、扩展性进行了广泛优化，并包含了可以在本地或者云设备上可以运行的点对点流程（Best practice）。

该版本得益于Broad研究所大规模运行基因组分析流程的科学和业务专家，来自业界Intel, Google Cloud, Cloudera, Microsoft Genmics, IBM Research, Amazon Web Services and Alibaba Cloud的工程师，都为GATK4的的开发做出来贡献。

2017成立的Intel-Broad基因组数据工程中心，Broad研究所的人员与Intel协同合作，对关键流程步骤做出了巨大优化。特别是Intel显著优化了基于GVCF的胚细胞joint-calling流程的扩展性，使得Broad团队可以在2个星期内完成15,000个全基因组样本的变异分析工作，而GATK3要处理3,000个全基因组样本需要至少6个星期。

https://software.broadinstitute.org/gatk/gatk4 https://github.com/broadinstitute/gatk http://jandan.net/2017/05/31/gatk4-open.html http://www.eeboard.com/news/gatk4/ http://ju.outofmemory.cn/entry/324861 https://gatkforums.broadinstitute.org/gatk/discussion/10502/gatk-4-0-will-be-released-jan-9-2018#latest