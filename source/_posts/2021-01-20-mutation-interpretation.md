---
title: 谈一谈在变异解读过程中用到的几个不太熟悉的预测指标
tags:
  - 帅旸
  - 解读
url: archives/1209.html
id: 1209
categories:
  - Default Category
date: 2021-01-20 10:25:23
---

帅旸谈一谈在变异解读过程中用到的几个不太熟悉的预测指标：

# z score

z score：这个指标指的是某个基因对missense的耐受程度，具体是指该基因所期望的missense数比上观察

到的missense数，如果z score>3.09，则认为该基因对missense不耐受，根据公式我们可以看出如果比值越大，则基因对missense越不耐受。利用z score可以在我们使用ACMG指南PP2的时候使用。

# REVEL score

REVEL score：ClinGen SVI建议使用REVEL用来预测missense致病性。与其他常用missense致病性预测软件不同，REVEL整合了包括SIFT、PolyPhen、GERP++在内的13个软件的预测结果，对罕见变异的预测结果更加出色。当REVEL score>0.75，<0.15时分别使用ACMG指南PP3和BP4。

# GERP++

GERP++ rejected substitutions” (RS) score：GERP++从基因进化速率角度预测位点保守性，具体是指该基因位点所期望的碱基替换次数减去观察到的碱基替换次数，可见分数越大，该位点保守性较强，当GERP++ RS score>6.8时，认为该位点保守。当分析一个不影响剪切的同义突变时，如果RS score<6.8，则可以使用ACMG指南BP7。

# dbscSNV score

dbscSNV score：dbscSNV含有两个不同的算法，用来预测变异是否影响截切，一个是基于adaptive boostin，一个是基于Random Forest。当两种算法得分均小于0.6时，则认为不影响剪切。

# 参考

ClinGen及Zhang, J., Yao, Y., He, H., & Shen, J. (2020). Clinical Interpretation of Sequence Variants. Current Protocols in Human Genetics, 106(1), e98.

其他参数如pLI及 Haploinsufficiency score我们之前已经介绍过，请点击下文链接

http://www.zxzyl.com/archives/940

\#####################################################################
\#版权所有 转载请告知 版权归作者所有 如有侵权 一经发现 必将追究其法律责任
\#Author: 帅旸
\#####################################################################