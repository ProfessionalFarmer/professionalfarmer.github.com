---
title: 甲基化芯片中的M值和B值
tags:
  - Chip
  - Methylation
url: archives/1129/index.html
id: 1129
categories:
  - Default Category
date: 2020-09-11 06:08:23
---

M值和B值的计算公式

![](/wp/f4w/2020/2020-09-10-M-B-value1.png)

[https://link.springer.com/article/10.1186/s41241-017-0041-9](https://link.springer.com/article/10.1186/s41241-017-0041-9)

## The relationship curve between M-value and Beta-value

M值和B值的对应关系

![](/wp/f4w/2020/2020-09-10-M-B-value2.jpg)


## The histograms of Beta-value (left) and M-value (right) (27578 interrogated CpG sites in total)

M值和B值的分布

![](/wp/f4w/2020/2020-09-10-M-B-value3.jpg)

minfi包有getM和getBeta来分别计算M-values和Beta-values，包的作者认为，

- M-values具有更好的统计特性，更适合用于进行下游的统计分析（差异分析等）
- Beta-values更加容易解释，更能说明生物学上的意义
- 
CHAMP包在load的时候，可以指定计算Beta-value还是M-value

一般来说，具体的β值的意义是：

- 任何等于或大于0.6的β值都被认为是完全甲基化的
- 任何等于或小于0.2的β值被认为是完全未甲基化的
- β值在0.2和0.6之间被认为是部分甲基化的。


参考：

[https://zhuanlan.zhihu.com/p/108364645](https://zhuanlan.zhihu.com/p/108364645)

[https://link.springer.com/article/10.1186/s41241-017-0041-9](https://link.springer.com/article/10.1186/s41241-017-0041-9)

