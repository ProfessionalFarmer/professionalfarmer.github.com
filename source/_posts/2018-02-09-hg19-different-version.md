---
title: hg19、GRCH37、b37、hs37d5介绍和区别
tags:
  - Genome
url: archives/829.html
id: 829
categories:
  - Default Category
date: 2018-02-09 15:37:02
---


大家经常用UCSC的hg19和NCBI的GRCh37版本的，但还有其他的版本，比如b37，hg37d5，比如在分析NIST的genome in a bottle（GIAB）提供的bam数据时，就遇到了hg37d5的版本，在用GATK的时候会遇到b37版本。

# GRCh37

Genome Reference Consortium(基因组参照序列联盟)，由英国Wellcome Trust Sanger研究中心（the Wellcome Trust Sanger Center）、华盛顿大学基因组中心（The Washington University Genome Center）、欧洲生物信息研究所（the European Bioinformatics Institute）和美国国家生物技术信息中心（NCBI）联合组成。

GRCH37版本发布之后，也会有小的更新，比如GRCh37.p2，大的更新比如由GRCh37升级到GRCh38，填补gap，修改部分序列，其目的是提供一个完整的基因组序列assemble。GRCh38已经在2013年发布，多数基因组数据库正在兼容或者更新到该版本。

该版本包含人类chr1到chr22，chrX，chrY，MT染色体以及

*   "unlocalized sequences"：知道来自哪条染色体但不知道具体位置的序列
*   "unplaced sequences"：知道来自人类基因组序列，但不知道与染色体的关系
*   "alternate loci"：来自基因组特定区域，代表该区域序列的多样性
"1" to "22", "X", "Y" and "MT"命名比较规范，ENSEMBL， genome browser， the NCBI dbSNP (in VCF files), the Sanger COSMIC (in VCF files),都依照该规范。

下载地址：ftp://ftp.ncbi.nih.gov/genomes/Homo_sapiens

# GRCh37lite

只包含GRCh37版本中的chr1到chr22，chrX，chrY，MT染色体

下载地址：ftp://ftp.ncbi.nih.gov/genbank/genomes/Eukaryotes/vertebrates_mammals/Homo_sapiens/GRCh37/special_requests/

# hg19

UCSC提供，容易下载，因为UCSC方便下载各种坐标文件（bed，gtf等），该版本可以与这些坐标对应。与GRCh38对应的是hg38版本。

该版本序列包括chr1到chr22，chrX，chrY序列与GRCh37完全一致（完全一致，完全一致），线粒体序列稍微不一样，以及
- "chr*_random sequences" 知道来自哪条染色体但不知道具体位置的序列
- "chrUn_* sequences" 知道来自人类基因组序列，但不知道与染色体的关系

UCSC与GRCh不同的地方有：
- 在重复区域repeat region有小写来表示，这点和GRCh不同
- 此外染色体有chr前缀，而GRCh没有chr前缀。
- 线粒体序列版本不一样

下载地址：ftp://hgdownload.cse.ucsc.edu/goldenPath/hg19/chromosomes

# b37

来自1000 Genome第一阶段，被称为b37（GATK和IGV社区小组中经常使用），包含了GRCh37, the rCRS mitochondrial sequence（MT序列）
unlocalized sequences和unplaced sequences以他们的检索号命名，比如"GL000191.1", "GL000194.1", etc.
但是不（不不不）包含 alternate loci

下载地址：ftp://ftp.broadinstitute.org/pub/seq/references

# hs37d5

可以理解成b37的升级版，在1000 Genome第二阶段使用。该版本包含了b37数据，以及
- human herpesvirus 4 type 1 sequence 人类疱疹病毒序列("NC_007605") 
- "decoy" sequence诱饵序列（名为hs37d5） 来自HuRef、BAC或者质粒克隆和NA12878，可以提高序列比对的正确率 
- 此外在Y染色体上的性染色体同源区域PAR标为N碱基，这样对应的X染色体的区域当作二倍体 

这些更改有利于序列比对和突变检测，降低假阳性与b37兼容。

PS：正如以前讲到的（文章《思考在比对时，关于是否将chr*_random和chrUn_*序列放在参考基因组中的思考》），序列比对不要只放chr1到chr22，chrX，chrY和MT（我见过国内知名测序公司有这么干的），其他序列和诱饵序列非常重要，可以提高比对的准确率，降低假阳性。

详情见：ftp://ftp.1000genomes.ebi.ac.uk/vol1/ftp/technical/reference/phase2_reference_assembly_sequence/hs37d5.slides.pdf
下载地址：ftp://ftp.1000genomes.ebi.ac.uk/vol1/ftp/technical/reference/phase2_reference_assembly_sequence

# 参考

http://googlegenomics.readthedocs.io/en/latest/use_cases/discover_public_data/reference_genomes.html
https://wiki.dnanexus.com/Scientific-Notes/human-genome

\#####################################################################
\#版权所有 转载请告知 版权归作者所有 如有侵权 一经发现 必将追究其法律责任
\#Author: Jason
\#####################################################################