---
title: 分类模型的性能评估
tags:
  - Machine learning
  - Model
  - Performance 
url: archives/1102/index.html
id: 1104
categories:
  - Default Category
date: 2020-06-04 16:17:23
---

最常用的就是灵敏度和特异性，不过还有其他的，比如阴性预测值(negative predictive value, NPV)。

[![](/wp/f4w/2020/2020-06-04-ROC.gif)](https://raw.githubusercontent.com/ProfessionalFarmer/f4w/master/2020/2020-06-04-ROC.gif)

通常，先画一个ROC曲线，计算曲线下面积。ROC上的每个点是特定阈值下，分类的sensitivity和specificity，没多点连起来组成ROC，曲线下面积就是AUC。面积越大越好，如果AUC是1，说明模型能够完全区分要预测的类别。

如果不是1，就要考虑阈值取哪里比较好，这里就涉及到Youden index。Youden index 其实就是为了找到使得sensitivity和specificity之和最大max(sensitivities+specificities)的阈值。

另外就是考虑其他指标来评估分类模型的性能：specificity, sensitivity, accuracy, npv, ppv, precision, recall, tpr, fpr, tnr, fnr, fdr。这些指标可谓琳琅满目，不过这之间有重复的，如下，都是基于tn（真阴）, tp（真阳）, fn（假阴）, fp（假阳）的个数进行计算。

| 　   |    | 预测 |    |
|------|:--:|:----:|----|
| 　   | 　 |   P  |  N |
| 实际 |  P |  TP  | FN |
|      |  N |  FP  | TN |

因为经常用到，就罗列了一下。

|             | 具体描述                            | 公式           | 别名                |
|-------------|-------------------------------------|----------------|---------------------|
| tn          | True negative count真阴数           | –              | –                   |
| tp          | True positive count真阳数           | –              | –                   |
| fn          | False negative count假阴数          | –              | –                   |
| fp          | False positive count假阳数          | –              | –                   |
| specificity | Specificity特异度                   | tn / (tn + fp) | tnr                 |
| sensitivity | Sensitivity灵敏度                   | tp / (tp + fn) | recall, tpr         |
| accuracy    | Accuracy正确率                      | (tp + tn) / N  | –                   |
| npv         | Negative Predictive Value阴性预测值 | tn / (tn + fn) | –                   |
| ppv         | Positive Predictive Value阳性预测值 | tp / (tp + fp) | precision           |
| precision   | Precision精准率                     | tp / (tp + fp) | ppv                 |
| recall      | Recall正确率                        | tp / (tp + fn) | sensitivity, tpr    |
| tpr         | True Positive Rate真阳性率          | tp / (tp + fn) | sensitivity, recall |
| fpr         | False Positive Rate假阳性率         | fp / (tn + fp) | 1-specificity       |
| tnr         | True Negative Rate真阴性率          | tn / (tn + fp) | specificity         |
| fnr         | False Negative Rate假阴性率         | fn / (tp + fn) | 1-sensitivity       |
| fdr         | False Discovery Rate伪发现率        | fp / (tp + fp) | 1-ppv               |


