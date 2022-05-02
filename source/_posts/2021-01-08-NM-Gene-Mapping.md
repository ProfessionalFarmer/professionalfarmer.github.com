---
title: Map NM ID to Gene Symbol
tags:
  - ID
url: archives/1195.html
id: 1195
categories:
  - Default Category
date: 2021-01-08 16:39:23
---

新年快乐，21年的第一篇文章。

以前写过映射ENSEMBL ID 和 NCBI ID， [http://www.zxzyl.com/archives/736](http://www.zxzyl.com/archives/736)。

日常分析中，我们也会经常遇到其他的ID mapping的工作，这种工作不是基因ID转基因ID，而是转录本的ID转基因ID。

如果用的是refGene的注释，最简单了，直接用下面的命令即可

```
mysql --user=genome -N --host=genome-mysql.cse.ucsc.edu -A -D hg38 -e "select name,name2 from refGene"
```

不过我也经常通过解析gtf文件获得，因为gtf有转本的ID，也有基因的symbol或者ID，只要有gtf文件就可以提取。本着不造轮子的精神，我利用的是现成的R包
```
library(plyranges)
gr <- read_gff("/path/to/gtf/or/gff") %>% select(transcript_id, gene_id, gene_name)
gr <- unique(data.frame(gr))
```

我也在自己的包里面写了一个函数得到ensembl，refseq，hgnc，gene symbol的对应关系，biomaRt比较慢，可以把结果保存成文件
```R
devtools::install_github("ProfessionalFarmer/loonR")
# 需要安装biomaRt和dplyr
mapping.table <- loonR::get_full_mapping_table()
# 保存mapping.table

```

#####################################################################
#版权所有 转载请告知 版权归作者所有 如有侵权 一经发现 必将追究其法律责任
#Author: Jason
#####################################################################



