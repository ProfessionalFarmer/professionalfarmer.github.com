---
title: 通路富集分析计算显著性
tags:
  - Pathway
url: archives/733/index.html
id: 733
categories:
  - Default Category
date: 2016-01-30 10:54:42
---


## 富集分析

在组学分析中，会得到一组特定意义的基因集，比如差异表达基因集，然后这些基因分布在哪些通路上，是随机分布在各个通路上还是富集在了某个通路上，也就是富集分析。富集的通路往往与研究的生物学状态改变有关。

富集分析中统计的是基因数目，即**计数数据**，常用的检验方法有超几何分布和卡方检验，一般都推荐超几何分布检验。

### 1，超几何分布和Fisher's Exact Test

Fisher 精确检验又叫做超几何分布检验
超几何分布是统计学上一种离散概率分布。它描述了由有限个物件中抽出k个物件，成功抽出指定种类的物件的次数（不归还）。在富集分析中，可以理解为在基因组基因范围（N个）内，某个通路M个基因，抽出n个基因，其中抽到k个基因在此通路上的概率。

非差异表达基因 差异表达基因
注释到A通路 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 20 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;50
没有注释到A通路 &nbsp; 1870 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 80

![hypergeometrix超集合分布](/wp/f4w/2020/2016-01-29-hypergeometrix-function.png)

### 2，卡方检验 x2

卡方检验就是统计样本的实际观测值与理论推断值之间的偏离程度，实际观测值与理论推断值之间的偏离程度就决定卡方值的大小，卡方值越大，越不符合，偏差越小，卡方值就越小，越趋于符合，若量值完全相等时，卡方值就为0，表明理论值完全符合。

![Chi-Square卡方检验](/wp/f4w/2020/2016-01-29-x2-Chi-Square-function.png)

fi是实际频数，npi是理论频数。

Ref http://blog.sina.com.cn/s/blog_670445240101m4z3.html
Ref [https://en.wikipedia.org/wiki/Fisher%27s_exact_test](https://en.wikipedia.org/wiki/Fisher%27s_exact_test "https://en.wikipedia.org/wiki/Fisher%27s_exact_test")

\#####################################################################
\#版权所有 转载请告知 版权归作者所有 如有侵权 一经发现 必将追究其法律责任
\#Author: Jason
\#####################################################################