---
title: Combining dependent P-values合并多个检验的p-value
tags:
  - Test
  - Statistic
url: archives/1133/index.html
id: 1133
categories:
  - Default Category
date: 2020-09-12 18:25:23
---
今天在看文章的时候，发现原来p-value也可以合并。比如一个基因在不同组学数据的检验中对应了多个p-value，可以合并成一个。

常用的是Fisher's method,

![](/wp/f4w/2020/2020-09-11-Fisher method.svg)

-2[ln(P1) + ln(P2) + ... + ln(Pi)]符合X2分布（自由度为2k，k为p-value的个数）。

还有Brown’s methods和 Kost’s methods，具体的介绍如下图。

![](/wp/f4w/2020/2020-09-11-Combining dependent P-values.png)


参考：

[https://academic.oup.com/bioinformatics/article/32/17/i430/2450768](https://academic.oup.com/bioinformatics/article/32/17/i430/2450768)

[https://www.nature.com/articles/s41467-019-13983-9](https://www.nature.com/articles/s41467-019-13983-9)

#####################################################################
#版权所有 转载请告知 版权归作者所有 如有侵权 一经发现 必将追究其法律责任
#Author: Jason
#####################################################################