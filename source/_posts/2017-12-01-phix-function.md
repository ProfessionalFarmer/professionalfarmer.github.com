---
title: 测序中加入Phix的作用
tags:
  - Illumina
  - Phix
  - Sequencing
url: 789.html
id: 789
categories:
  - Default Category
date: 2017-12-01 23:40:54
---

测序建库的时候，会加入一定比例的Phix，那么Phix文库有什么作用呢，我转了两篇文章，方便大家理解。Phix文库最主要的目的1）是调节碱基平衡，改善测序仪的空间校正，便于后期提高base calling的准确性，2）由于Phix序列已知基因组较小，在测序的过程中Illumina的测序仪就开始将测的read与phix基因组进行比较，预估测序指标。我也遇到过，Illumina工程师在维护测序仪时，用Phix文库测试。转载内容详见下文

<!--more-->

# 转自Illumina公司

PhiX对照品v3是一款可靠、连接接头的文库，适合用作Illumina测序运行的对照品。该文库来源于已妥善分析特征的小型PhiX基因组，并具备多项测序和比对优点。

通用型PhiX对照品v3不仅能用作即用型文库，还可用于多种应用，以增加工作流程价值及提高结果的可信度。

**PhiX文库提供适用于簇生成、测序和比对的质量对照品，以及适用于串扰矩阵生成、定相和预定相的校正对照品。可快速对其进行比对以预估相关边合成边测序(SBS)指标，比如定相和错误率**。

视乎应用，PhiX对照品v3还可用作：

- 适用于碱基不均衡样本（AT或GC内容低于40%或高于60%的基因组）的高浓度外标对照品

- 低浓度掺入，适用于比对和定量效率的计算

- 可在多样性较低样本旁的设置照品通道

- 适用于簇生成问题故障诊断，便于确定错误是否与文库制备有关

# 转自Mars-Zhan老师

测定混合微生物群的16S的若干个片段，从其可变区的序列来进行菌落组成分序，已是很常用的实验方法。

自从MiSeq测序平台推出PE300的测序方式之后，用PE300来测16S的V1、V2、V3区，已成了最常用的菌落分析手段。

但是每次我提醒用户：在做16S文库测序的上机时，建议加入70%的PhiX文库。用户都会感到不解：为什么要浪费这70%的测序通量？

这还要从Illumina公司的测序原理说起：

Illumina的测序根本原理是用4种颜色荧光基团标记4种dNTP。

在显微扫描镜下，通过对4种颜色的荧光进行分别扫描，得到4张照片，每张照片对应于一种颜色的荧光。

把4张照片进行对比，把各张照片上的光点重合，计算每个光点的光的颜色强度，倒过来推算出这个点是哪种荧光基团，进尔再推算出这个点是哪种碱基。

MiSeq测16S文库时，为什么要加PhiX?

但请注意，因为这4张照片都是纳米级的分辨率，而测序过程中芯片是移动的，所以每次拍照多少存在一定程度的空间偏差，如上图所示。这就需要进行空间校正。

文库复杂度不够高带来的影响：

如果是文库的复杂度足够高，也就是在一个测序循环中，A/C/G/T四种碱基的比例较接近于各25%，那么4张照片上都会有足够多的明亮的光点，可供空间校正之用。

但是如果文库的复杂度不够高，典型的例子就是PCR扩增产物，比如说第一个循环，99%的 碱基都是A，那么C/G/T三种碱基加起来也只有1%。这就导致C/G/T这三张照片都很暗，上面没有足够多的光点可供测序仪来分辨，**更难于做空间校正**。 测序仪就会把大多数无法准确分辨的点给舍弃。

最终的结果就是：测序得到的有效数据量（PF data，Pass Filter data）很少，而且数据的质量（Q值）也偏低。

上述的原因，让Illumina的MiSeq和HiSeq 2000/2500在测复杂度低的文库（PCR扩增文库、Bisulfite处理的甲基化文库、简化基因组文库等）时，如果没有加入弥补的方法，软件就不 能很好识别的光点，导致最后的有效数据量减少、测序数据质量也偏低。

目前的解决方案是：

在测低复杂度的文库时，掺入一定量的高复杂度文库。最常用的掺入文库是Illumina出品的PhiX文库，也有些实验室会用哺乳类动物的基因组文库来增加文库的复杂度，效果是一样的。

**PhiX文库有以下的特点**：

PhiX文库中GC含量约为45%，是碱基比例较为平衡的样本。

PhiX DNA就是ΦX174噬菌体的DNA，其基因组的长度是4kb略多，其序列已清楚地被测定。

PhiX DNA文库没有Index，所以在样本Demultiplex的过程中，被挪到undetermined的文件中，不会与别的有Index的文库相混。

PhiX的序列是已知的，所以，在测序过程中，**仪器会对PhiX的序列进行比对**，算出Phasing和Pre-Phasing(一个簇中，有多少比例的DNA是少合成了一个碱基（Phasing），又有多少比例的DNA是多合成了一个碱基（Pre-Phasing）)

转自陈云地老师

常见的碱基组成不平衡的样本类型比如：甲基化、扩增子、转录组、ChIP、重复序列测序（16S rDNA, HLA...）等等，其中重亚硫酸盐处理后的甲基化样本是碱基组成极度不平衡的，基本没有C，只有A、T、G三种碱基，而T的含量又比正常样本增加几乎一倍。

碱基不平衡的样本可以与碱基平衡的样本混合以**改善平衡程度**，常见碱基平衡的样本比如人全基因组、人外显子组、Illumina标准品文库PhiX等。

平衡与不平衡样本的混合比例，根据样本的不平衡的严重程度调整。样本的碱基越不平衡，Phix文库的比例越高。

其中PhiX可以同时起到两个作用：**改善碱基平衡度，作为阳性对照监控测序操作是否成功**。

http://blog.sina.com.cn/s/blog_751bd9440102vruh.html

http://garification.blog.163.com/blog/static/1741330252015726502943/

https://www.illumina.com.cn/products/by-type/sequencing-kits/cluster-gen-sequencing-reagents/phix-control-v3.html