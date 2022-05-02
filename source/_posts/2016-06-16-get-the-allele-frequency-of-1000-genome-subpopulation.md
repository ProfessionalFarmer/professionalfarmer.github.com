---
title: Get the allele frequency of 1000 Genome subpopulation
tags:
  - 1000 Genome
  - Frequency
url: archives/761.html
id: 761
categories:
  - Default Category
date: 2016-06-16 15:36:10
---

在1000genome的FTP服务器上可以下载一个all的vcf文件，里面可以看到AFR, AMR, EAS, EUR, SAS人群的allele频率，但是该种族下面的亚群的频率信息需要在[http://grch37.ensembl.org](http://grch37.ensembl.org)搜索得到，比如 [http://grch37.ensembl.org/Homo_sapiens/Variation/Population?db=core;r=1:230845294-230846294;v=rs699;vdb=variation;vf=102788013](http://grch37.ensembl.org/Homo_sapiens/Variation/Population?db=core;r=1:230845294-230846294;v=rs699;vdb=variation;vf=102788013) ，还有一种方式，就是下载包含所有样本的突变信息的VCF文件，利用vcftools计算。

The allele frequency of super population (AFR, AMR, EAS, EUR, SAS, see [http://www.1000genomes.org/category/population/](http://www.1000genomes.org/category/population/)) can be obtained from [all.vcf](ftp://ftp.1000genomes.ebi.ac.uk/vol1/ftp/release/20130502/ALL.wgs.phase3_shapeit2_mvncall_integrated_v5b.20130502.sites.vcf.gz).

However, the allele population frequency in subpopulation is not well obtained.

One way is search the web [http://grch37.ensembl.org](http://grch37.ensembl.org) by rs identifier, E.g. [http://grch37.ensembl.org/Homo_sapiens/Variation/Population?db=core;r=1:230845294-230846294;v=rs699;vdb=variation;vf=102788013](http://grch37.ensembl.org/Homo_sapiens/Variation/Population?db=core;r=1:230845294-230846294;v=rs699;vdb=variation;vf=102788013) .

Another way is calculated on your local machine. The following will introduce how to get allele frequency of CHB population in chr1 chromosome. CHB Han Chinese in Beijing

# Prepare file and software dependency

panel file contains sample information

panel file: [integrated_call_samples_v3.20130502.ALL.panel](ftp://ftp.1000genomes.ebi.ac.uk/vol1/ftp/release/20130502/integrated_call_samples_v3.20130502.ALL.panel) 

vcf file contains allele information of all samples

chr1.vcf: [ALL.chr1.phase3_shapeit2_mvncall_integrated_v5a.20130502.genotypes.vcf](ftp://ftp.1000genomes.ebi.ac.uk/vol1/ftp/release/20130502/ALL.chr1.phase3_shapeit2_mvncall_integrated_v5a.20130502.genotypes.vcf.gz)

Also, you should install vcftools.

```bash
wget ftp://ftp.1000genomes.ebi.ac.uk/vol1/ftp/release/20130502/integrated_call_samples_v3.20130502.ALL.panel
wget ftp://ftp.1000genomes.ebi.ac.uk/vol1/ftp/release/20130502/ALL.chr1.phase3_shapeit2_mvncall_integrated_v5a.20130502.genotypes.vcf.gz
git clone https://github.com/vcftools/vcftools.git
cd vcftools/ 
./autogen.sh 
./configure 
make 
make install
cd ..
```



<!--more-->

# Calculate allele frequency of CHB population

```
grep CHBintegrated_call_samples_v3.20130502.ALL.panel ' cut -f1 > CHB.samples.list
vcf-subset -c CHB.samples.list ALL.chr1.phase3_shapeit2_mvncall_integrated_v5a.20130502.genotypes.vcf.gz ' fill-an-ac ' bgzip -c > CHB.chr1.phase1.vcf.gz 
# Once you have this file you can calculate your frequency by dividing AN (allele number) by AC (allele count)
# or continue, vcftools --freq option will generate a .fre file
vcftools --gzvcf CHB.chr1.phase1.vcf.gz --freq --out CHB
```





# Result

<pre>head CHB.frq 
CHROM   POS     N_ALLELES       N_CHR   {ALLELE:FREQ}
1       10177   2       206     A:0.660194      AC:0.339806
1       10235   2       206     T:1     TA:0
1       10352   2       206     T:0.572816      TA:0.427184
1       10505   2       206     A:1     T:0
1       10506   2       206     C:1     G:0
1       10511   2       206     G:1     A:0
1       10539   2       206     C:1     A:0
1       10542   2       206     C:1     T:0
1       10579   2       206     C:1     A:0</pre>


Because every sample has two chromosomes, so N_CHR = N_sample * 2

Reference:

Population structure

[http://www.1000genomes.org/category/population/](http://www.1000genomes.org/category/population/)

[http://www.1000genomes.org/faq/how-can-i-get-allele-frequency-my-variant/](http://www.1000genomes.org/faq/how-can-i-get-allele-frequency-my-variant/)

\#####################################################################
\#版权所有 转载请告知 版权归作者所有 如有侵权 一经发现 必将追究其法律责任
\#Author: Jason
\####################################################################