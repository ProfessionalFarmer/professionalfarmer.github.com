---
title: 蛋白延伸（extension）变异的hgvs命名
tags:
  - HGVS
  - Mutation
  - Variant
url: archives/1447.html
id: 1447
categories:
  - Default Category
date: 2022-04-25 12:06:20
---
翻译[https://varnomen.hgvs.org/recommendations/protein/variant/extension/](https://varnomen.hgvs.org/recommendations/protein/variant/extension/)

这个突变类型不常见，hgvs的命名挺有意思的

# 延伸突变定义
序列变化导致参考氨基酸序列在N或者C端多了一个或者多个氨基酸

# 描述 

## p.Met1ext-5
N端格式: “prefix”“Met1”“ext”“position_new_initiation_site”, e.g. p.Met1ext-5

“prefix” = 前缀，用p.表示
“Met1” = 正常的翻译起始位点Met1
“ext” = 变化类型是延伸ext
“position_new_initiation_site” = 上游新的翻译起始位点-5

## e.g. p.Ter110GlnextTer17

C端格式：“prefix”“Ter_position”“new_amino_acid”“ext”“Ter”“position_new_termination_site”, e.g. p.Ter110GlnextTer17

“prefix” = 前缀，用p.表示
“Ter_position” = 正常的终止位点Ter110
“new_amino_acid” = 在终止位点编码的新的氨基酸Gln
“ext” = 变化类型是延伸ext
“Ter” = 终止位置Ter（或者用\*表示）
“position_new_termination_site” = 下游新的终止位点17

# 注意

<!--more-->

预测的序列，例如没有实验证据，应用括号括起来，e.g. p.(Ter110GlnextTer17) or p.(\*110Glnext\*17)

影响翻译起始位点的突变（Met1）导致上游（N端）翻译起始位点，描述为deletion-insertion, 导致下游 (C-terminal)翻译起始的描述为deletion

优先级: (1) extension, (2) frame shift or deletion-insertion.

# Examples

## p.Met1ext-5
突变在上游5'UTR导致一个新的翻译起始位点Met-5，是p.Met1extMet-5的改版


## p.Met1_Leu2insArgSerThrVal
突变造成上游产生一个新的翻译起始位点Met-4,实际表现为Met1和Leu2中插入ArgSerThrVal，氨基酸Met1变为了Val。这种通常不描述为延伸，因为Met1作为正常的氨基酸序列发生了变化。


## p.Ter110GlnextTer17 (natively p.\*110Glnext\*17)

发生在110位置终止密码子Ter(\*)，变为了一个非终止的Gln密码子，C端增加了若干氨基酸，在下游17位置产生新的密码子

## p.(Ter315TyrextAsnLysGlyThrTer) (p.\*315TyrextAsnLysGlyThr\*)
在315位置的终止密码子变成了非终止的Tyr，并增加几个氨基酸，在下游5号位生成新的终止密码子。

## p.Ter327Argext\*? (p.\*327Argext\*?)
327号位的终止密码子变成了Arg，但是造成了移码，且移码框内没有终止密码

# Q&A
## 蛋白层面的变化如何直接影响翻译起始密码子？
这类突变成为起始缺失突变，两种蛋白延伸突变的一种，发生在N端。但不同于密码子获得突变，因为这类突变没有直接影响正常的翻译起始密码子。

## 蛋白层面的变化如何直接影响翻译终止密码子？
这类突变成为非终止突变或者终止缺失突变，另外一个蛋白延伸突变的类型，发生在C端。

## 没有新的终止密码子产生时如何描述
这种突变用，比如p.Ter789ArgextTer?，用extTer?来表示没有新的终止密码子

## 5'UTR有新的起始密码子时如何描述
在DNA水平描述，例如c.-23A>T (导致 c.-25 caGggt c.-19 变为 caTggt, 产生新的ATG)。在RNA水平 r.-23a>u，在蛋白水平p.(Met1ext-8), 表明预测的蛋白序列在N端延伸了8个氨基酸。

## 把终止密码子TGA变为TGGA描述为移码还是延伸
这类突变在C端延伸了氨基酸序列，因此定义为延伸extension。

# 作业

下面这个突变我们命名为p.Ter863GlyextTer2或者p.\*863Glyext\*2

![](/wp/f4w/2022/2022-04-25-ExtensionVarianteAtProteinLevel.png)

#####################################################################
\#版权所有 转载请告知 版权归作者所有 如有侵权 一经发现 必将追究其法律责任
\#Author: Jason
#####################################################################