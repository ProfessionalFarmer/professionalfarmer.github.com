---
title: Convert gtf to bed12 format --- gtf2bed
tags:
  - bed
  - gtf
  - gtf2bed
url: archives/768.html
id: 768
categories:
  - Default Category
date: 2016-08-30 21:29:32
---

Some software requires bed12 format, not gtf/gff. So a convertion work should be done.

# bedops gtf2bed

Easy way to get your result ---- [bedops](http://bedops.readthedocs.io)

```
gtf2bed < Homo_sapiens.GRCh38.85.gtf ' head
1       11868   14409   ENST00000456328 0       +       11868   14409   0       3       359,109,1189,   0,744,1352,
1       12009   13670   ENST00000450305 0       +       12009   13670   0       6       48,49,85,78,154,218,    0,169,603,965,1211,1443,
1       17368   17436   ENST00000619216 0       -       17368   17436   0       1       68,     0,
1       14403   29570   ENST00000488147 0       -       14403   29570   0       11      98,34,152,159,198,136,137,147,99,154,37,        0,601,1392,2203,2454,2829,3202,3511,3864,10334,15130,
1       29553   31097   ENST00000473358 0       +       29553   31097   0       3       486,104,122,    0,1010,1422,
1       30266   31109   ENST00000469289 0       +       30266   31109   0       2       401,134,        0,709,
1       30365   30503   ENST00000607096 0       +       30365   30503   0       1       138,    0,
1       34553   36081   ENST00000417324 0       -       34553   36081   0       3       621,205,361,    0,723,1167,
1       35244   36073   ENST00000461467 0       -       35244   36073   0       2       237,353,        0,476,
1       52472   53312   ENST00000606857 0       +       52472   53312   0       1       840,    0,
```


Here we use UCSC's package to convert gtf format file to bed12 format file.

#  Download UCSC package

```shell
wget -c http://hgdownload.cse.ucsc.edu/admin/exe/linux.x86_64/gtfToGenePred
wget -c http://hgdownload.cse.ucsc.edu/admin/exe/linux.x86_64/genePredToBed
chmod 755 gtfToGenePred genePredToBed
```




## Convert gtf to bed12

```
time gtfToGenePred Homo_sapiens.GRCh38.85.gtf test.genePhred && genePredToBed test.genePhred result.bed && rm test.genePhred 

real    0m14.959s
user    0m14.387s
sys     0m0.567s
```

```
head reult.bed 
1       11868   14409   ENST00000456328 0       +       14409   14409   0       3       359,109,1189,   0,744,1352,
1       12009   13670   ENST00000450305 0       +       13670   13670   0       6       48,49,85,78,154,218,    0,169,603,965,1211,1443,
1       14403   29570   ENST00000488147 0       -       29570   29570   0       11      98,34,152,159,198,136,137,147,99,154,37,       0,601,1392,2203,2454,2829,3202,3511,3864,10334,15130,
1       17368   17436   ENST00000619216 0       -       17436   17436   0       1       68,     0,
1       29553   31097   ENST00000473358 0       +       31097   31097   0       3       486,104,122,    0,1010,1422,
1       30266   31109   ENST00000469289 0       +       31109   31109   0       2       401,134,        0,709,
1       30365   30503   ENST00000607096 0       +       30503   30503   0       1       138,    0,
1       34553   36081   ENST00000417324 0       -       36081   36081   0       3       621,205,361,    0,723,1167,
1       35244   36073   ENST00000461467 0       -       36073   36073   0       2       237,353,        0,476,
1       52472   53312   ENST00000606857 0       +       53312   53312   0       1       840,    0,
```


Cheers. 

# Another tool

I also recommend a perl script -- [gtf2bed](https://github.com/ExpressionAnalysis/ea-utils/blob/master/clipper/gtf2bed). This script works fine to convert gtf to bed format. Thanks for ea-utils project.

# Ref

[https://groups.google.com/a/soe.ucsc.edu/forum/#!topic/genome/fTNuZOS-CYA](https://groups.google.com/a/soe.ucsc.edu/forum/#!topic/genome/fTNuZOS-CYA)

[https://expressionanalysis.github.io/ea-utils/](https://expressionanalysis.github.io/ea-utils/)

[bedops.readthedocs.io](http://bedops.readthedocs.io)

\#####################################################################
\#版权所有 转载请告知 版权归作者所有 如有侵权 一经发现 必将追究其法律责任
\#Author: Jason
\####################################################################