---
title: 更新Bioconductor包--update a Bioconductor package
tags:
  - R
url: archives/765.html
id: 765
categories:
  - Default Category
date: 2016-08-01 22:07:58
---

A  package belong to Bioconductor  was updated (major revision) and released. I want to use the up to date package while in analysing. I am willing to use the new feature, so I need to update this  package. I had tried many ways and many times, and finally found a possible way.

更新Bioconductor中的特定包到最新版本。需要首先更新R，其次更新Bioconductor，最终更新包。

## 1, First your should update your R version

```
sudo apt-get update
sudo apt-get install r-base
```


This will allow the latest Bioconductor to work compitablly.

## 2， Second update Bioconductor

```
>remove.packages("BiocInstaller")  
source("http://bioconductor.org/biocLite.R") 
biocLite()  
```

\# this will fix an error:  Error: Bioconductor version *** cannot be upgraded with R version ***
\# install latest BiocInstaller
\# update Bioconductor

## 3，Third update your target package

```
emove.packages("package-name")   
biocLite("package-name")  
```

\# remove old version
\#  install the latest version 

\#####################################################################
\#版权所有 转载请告知 版权归作者所有 如有侵权 一经发现 必将追究其法律责任
\#Author: Jason
\####################################################################