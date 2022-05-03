---
title: 如何获取Ensembl gene id和NCBI的gene id及与HGNC的对应关系
tags:
  - Biomart
  - Ensembl
  - ID
  - NCBI
url: archives/736/index.html
id: 736
categories:
  - Default Category
date: 2016-02-17 23:12:13
---


Ensembl和NCBI都是盛名的基因组研究机构，提供相关的基因组结构注释文件，比如gtf或者gff，但注释的id却不是统一的。比如基因ID，Ensembl有Ensembl gene id，NCBI有entrez gene id。不同的人用的基因注释文件来源不同，就需要进行转换。本文主要讲如何利用Ensembl的Biomart，下载对应关系。

[Biomart](http://www.biomart.org/ "http://www.biomart.org/")整合了各种生物学注释数据，提供了易于操作的界面，在线提供批量下载，以加速科学研究。Ensembl已应用[biomart](http://asia.ensembl.org/index.html "http://asia.ensembl.org/index.html")提供相关服务。

The BioMart project provides free software and data services to the international scientific community in order to foster scientific collaboration and facilitate the scientific discovery process. The project adheres to the open source philosophy that promotes collaboration and code reuse.

Ensembl的biomart网址为[http://asia.ensembl.org/index.html](http://asia.ensembl.org/index.html "http://asia.ensembl.org/index.html")

## 第一步，选择相应的数据库

选择ensemble gene 83

![step1-select-database](/wp/f4w/2020/2016-02-17-ensembl-id-to-ncbi-entrez-gene-id/2016-02-17-step1-select-database.png) 

选择homo sapiens gene

![step1-select-database](/wp/f4w/2020/2016-02-17-ensembl-id-to-ncbi-entrez-gene-id/2016-02-17-step1-select-database-homoSapiens.png) 

<!--more-->

## 第二步，选择相应的attribute

点击attribute，选择ensembl中的ensembl gene id

![step2-attribute-select-ensemble-gene-id](/wp/f4w/2020/2016-02-17-ensembl-id-to-ncbi-entrez-gene-id/2016-02-17-step2-attribute-select-ensemble-gene-id.png) 

选择EXTERNAL中的EntrezGene ID，HGNC ID(s)，HGNC symbol，这里就是选择你想要的对应的数据。

![step2-attribute-select-external-link](/wp/f4w/2020/2016-02-17-ensembl-id-to-ncbi-entrez-gene-id/2016-02-17-step2-attribute-select-external-link.png)


## 第三步，查看数据条目

点击count，显示共66232个基因中的66232个基因被选中

![step3-click-count](/wp/f4w/2020/2016-02-17-ensembl-id-to-ncbi-entrez-gene-id/2016-02-17-step3-click-count.png)

## 第四步，查看或者下载数据

点击Results可以显示相关结果，可以指定每页显示的条目个数。如果有相对应的ID，则会显示。

![ensembl-id-to-ncbi-entrez-gene-id-result](/wp/f4w/2020/2016-02-17-ensembl-id-to-ncbi-entrez-gene-id/2016-02-17-step4-result-file.png)

此外可以保存为本地文件，选择保存为gz格式，tab分割（tsv），点击go即可下载到本地，gz文件中包含mart_export.txt文件。文件截图如下

![result](/wp/f4w/2020/2016-02-17-ensembl-id-to-ncbi-entrez-gene-id/2016-02-17-step4-result-file2.png)

Ref:
1, [http://www.biomart.org/](http://www.biomart.org/ "http://www.biomart.org/")

2，[http://asia.ensembl.org/biomart/martview](http://asia.ensembl.org/biomart/martview "http://asia.ensembl.org/biomart/martview")

\#####################################################################
\#版权所有 转载请告知 版权归作者所有 如有侵权 一经发现 必将追究其法律责任
\#Author: Jason
\#####################################################################