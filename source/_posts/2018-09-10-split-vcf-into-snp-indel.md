---
title: 将VCF文件中的突变拆分成SNP和INDEL
tags:
  - SNP
  - VCF
url: archives/1030.html
id: 1030
categories:
  - Default Category
date: 2018-09-10 11:14:45
---

# VCFTOOLS

得到SNP

```
vcftools --vcf X.vcf --remove-indels --out X.snps --recode --recode-INFO-all
```

得到INDEL

```
vcftools --vcf X.vcf --keep-only-indels --out X.indel --recode --recode-INFO-all
```



# GATK

得到SNP

```
java -jar GenomeAnalysisTK.jar \
    -T SelectVariants \
    -R reference.fasta \
    -V X.vcf   \
    -selectType SNP \
    -o X.snps.vcf
```




得到INDEL

```
java -jar GenomeAnalysisTK.jar \
    -T SelectVariants \
    -R reference.fasta \
    -V X.vcf  \
    -selectType INDEL \
    -o X.indel.vcf
```




本着有轮子不造轮子的原则，可以用VCFTOOLS和GATK来实现，当然如果想自己拆分的话，可以根据VCF中是否有SNP和INDEL的tag标签，或者根据ALT和REF中的碱基长度是否一致来实现拆分。

参考：

https://www.biostars.org/p/48204/
https://software.broadinstitute.org/gatk/documentation/tooldocs/3.8-0/org_broadinstitute_gatk_tools_walkers_variantutils_SelectVariants.php

\#####################################################################
\#版权所有 转载请告知 版权归作者所有 如有侵权 一经发现 必将追究其法律责任
\#Author: Jason
\#####################################################################