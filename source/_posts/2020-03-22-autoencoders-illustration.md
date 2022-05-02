---
title: 对Autoencoder(自编码器)的理解
tags:
  - AI
  - Machine learning
url: archives/1089.html
id: 1089
categories:
  - Default Category
date: 2020-03-22 14:18:10
---

通常数据的维度太大，可视化很难，也不利用模型的学习。有时候拿到数据做个PCA或者tSNE，就是把维度缩小到2维（当然也可以3维），便于看数据之间的关系。在机器学习中，Autoencoder也是一种降维的方式， Autoencoder输入层的神经元的数目和输出层的神经元的数目必须，而且要保证输出的结果尽最大可能和输入的结果一致。

![](/wp/f4w/2020/2020-03-30-Autoencoder.png)

图片来自网络

如上图所示，维度由大到小是decode过程，输出的结果可以从中间层经过encode得到，那么中间层保留了输入层的信息（因为输出层的结果从中间层得到），那么中间层的数据结果，就是降维后的结果，**可以拿来做其他事情**。 网络的复杂程度根据样本数设计。 无监督的聚类，便可以从中间层开始；数据的学习也可以从中间层开始。当输入层是多组学数据时，中间层便是融合后的结果。