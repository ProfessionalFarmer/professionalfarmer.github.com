---
title: 遗传解读遇到基因LoF或deletion可以从单倍剂量不足下手
tags:
  - Genetic Counseling
  - Haploinsufficient
  - Lof
url: archives/940/index.html
id: 940
categories:
  - Default Category
date: 2018-05-03 16:48:02
---


# 单倍剂量不足

最近在解读过程中，接触到一个新的名词-单倍剂量不足，它的英文名字叫做Haploinsufficiency。单倍剂量不足指一个等位基因突变或者缺失后后，另一个等位基因能正常表达，这种基因表达翻译后的蛋白水平只有正常的50%，但不足以维持正常的生理功能，导致特定表型出现。

导致单倍剂量不足的愿意可能有多种，比如一个基因的拷贝发生缺失，或者突变导致不能产生正常的mRNA，或者特殊情况下mRNA或蛋白质不稳定导致降解等。

与解读相关的是，单倍剂量不足现象是导致遗传病发生的一个原因，如果一个基因存在单倍剂量不足的机制，loss of fucntion或者gene deletion可能会导致疾病发生。具体到日常解读中，遇到LoF或者gene deletion，我们可以通过查询NCBI的ClinGen和ExAC的pLI（loss-intolerance）来查看基因是否存在单倍剂量不足，进而寻找可能致病的线索。

# ClinGen的Haploinsufficiency score

ClinGen有一个分级系统，根据Haploinsufficiency score的分级结果，预测基因功能缺失突变（LOF）或拷贝缺失与临床表型的相关性。ClinGen成立了EBR工作组，建立一个分级系统，用来系统评估CNVs的可能临床相关性，该分级系统参考以下内容：已报道的致病突变数，遗传方式，表型一致性，大规模case-control研究，致病机制，公共人群数据库，专家共识。并且会定期整合新的证据和重新评估。ClinGen评估了Loss of fucntion和triplosensitivity（基因发生duplicate），分数从0-3，分值越高则有更多的证据表明这个基因的剂量敏感导致相应临床表型。1表示少量证据表明与表型相关，3表示大量证据表明与表型相关，此外，针对剂量不敏感的基因，给40的score，引起AR疾病的基因，评分为30的score。

# ExAC的pLI

我们还得聊一聊另一个预测值pLI，它指的是基因对于LOF突变的不可忍受的可能性。The Exome Aggregation Consortium (ExAC) 通过分析60,706 不同族群的个体外显子数据，计算了pLI分值，来表示基因 不耐受Loss of Function (LoF) 突变。ExAC通过模型比较每个基因内观察到的罕见突变和期望的罕见突变数据，通过Z score量化这种偏离。编码区的长度来减少混杂因素，对于蛋白截断突变（Protein Truncating Variants (PTV) ），通过比较PTV在观察和期望中的数据，将基因分成3类。

**Null**, 观察约等于期望，对LoF突变耐受 where observed ≈ expected (LoF variation is tolerated) 
**Recessive**, 观察得到的小于期望的50%，杂合LoF耐受 where observed ≤ 50% of expected (heterozygous LoFs are tolerated)
**Haploinsufficient**, 观察得到的小于期望的10%，杂合LoF不耐受where observed < 10% of expected (heterozygous LoFs are not tolerated)



pLI分值是一个给定基因归类到Haploinsufficient 类别中的概率，也就是对LoF不耐受的分值。分值越高，越不耐受（intolerant），分值越低，越耐受（tolerant）。当然，具体运用中，不能仅根据pLI值就判定一个LOF突变的致病性，我们还要同时考虑如疾病发病年龄，外显率，Haploinsufficiency score等。

想了解跟多可以官网查看。
[https://www.ncbi.nlm.nih.gov/projects/dbvar/clingen/help.shtml](https://www.ncbi.nlm.nih.gov/projects/dbvar/clingen/help.shtml)
[https://decipher.sanger.ac.uk/info/loss-intolerance](https://decipher.sanger.ac.uk/info/loss-intolerance)

\#####################################################################
\#版权所有 转载请告知 版权归作者所有 如有侵权 一经发现 必将追究其法律责任
\#Author: 感谢好友SYY&33，& Jason
\#####################################################################