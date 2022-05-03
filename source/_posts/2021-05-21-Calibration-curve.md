---
title: 预测模型校准曲线 Calibration curve
tags:
  - Calibration
  - Model
url: archives/1256/index.html
id: 1256
categories:
  - Default Category
date: 2021-05-21 19:34:20
---



![](/wp/f4w/2021/2021-05-21-Calibration-Curve.png)

我们常用ROC曲线来衡量模型的预测能力，但很少关注模型的校准度calibration。

Calibration curve的**横坐标**是我们用模型预测的probability，比如我预测的是可能是肿瘤患者的概率，risk probability，**纵坐标**是真实的事件event的概率或者事件的proportion。



我们画图的时候，通常是点，需要进行平滑smooting，常用的是 **loess**方法。



如果我们预测的概率和真实的事件概率完全匹配，那么calibration plot则是一条斜率为1的直线（perfect calibration）。如果我们画出的先在perfect calibration上面，则表示underestimated，就是我们预测的风险或者概率低，真实情况却比较高；反之如果在perfect calibration在下，则是overestimated ，我们预测的风险比真实的风险要高。



根据吻合的程度，又分为poor calibration或者strong calibration，也可以做Hosmer–Lemeshow (HL) goodness-of-fit test。



参考：[https://bmcmedicine.biomedcentral.com/articles/10.1186/s12916-019-1466-7](https://bmcmedicine.biomedcentral.com/articles/10.1186/s12916-019-1466-7)

```
# rms包可以画calibration plot
library(rms)
val.prob(predicted.probability, TRUE.Label)

如果模型用rms建立的话，还可以用
rms::calibrate的方法

#我自己也参考别人写了一个函数,结果如下图，欢迎使用
library(loonR)
riskCalibrationPlot(TRUE.Label, predicted.probability)
```


![](/wp/f4w/2021/2021-05-21-Calibration-Curve-1.png)

#####################################################################
#版权所有 转载请告知 版权归作者所有 如有侵权 一经发现 必将追究其法律责任
#Author: Jason
#####################################################################

