---
title: Prepare a data frame for sample CNV data
tags:
  - CNV
  - R
url: archives/1091/index.html
id: 1091
categories:
  - Default Category
date: 2020-03-26 13:08:00
---

If we want to cluster samples based on CNV data, a dataframe is needed. However, CNV segments in each sample are not the same. Maybe overlap or distinct. I think CNTools package migh solve this challenge. An example is shown as below. The result is a **reduced segment** data frame.

```R
BiocManager::install("CNTools")
data("sampleData")
seg <- CNSeg(sampleData)
rdseg <- getRS(seg, by = "region", imput = FALSE, XY = FALSE, what = "mean") 
View(rdseg@rs)
```




Input dataframe has six columns ("ID","chrom","loc.start","loc.end","num.mark","seg.mean") including 277 samples and 54825 segments.

![](/wp/f4w/2020/2020-03-26-CNTools-Input.png)

The result can be got from rdseg@rs, like this

![](/wp/f4w/2020/2020-03-26-CNTools-Output.png) Cheers Also, we can use CNRegions from iClusterPlus package. CNregions(sampleData) 

Ref:
[https://www.rdocumentation.org/packages/CNTools](https://www.rdocumentation.org/packages/CNTools) [https://rdrr.io/bioc/iClusterPlus/man/CNregions.html](https://rdrr.io/bioc/iClusterPlus/man/CNregions.html)
\##################################################################### 
\#版权所有 转载请告知 版权归作者所有 如有侵权 一经发现 必将追究其法律责 
\#Author: Jason
\#################################################################