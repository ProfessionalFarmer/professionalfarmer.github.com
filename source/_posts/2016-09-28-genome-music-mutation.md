---
title: 利用genome music分析癌症样本中显著突变的基因和相关通路
tags:
  - Cancer
url: archives/770/index.html
id: 770
categories:
  - Default Category
date: 2016-09-28 20:41:56
---


MuSiC   the Mutational Significance In Cancer (MuSiC) suite of tools
官网地址 [http://gmt.genome.wustl.edu/packages/genome-music/index.html](http://gmt.genome.wustl.edu/packages/genome-music/index.html)

# 功能其主要功能

1. Apply statistical methods to identify significantly mutated genes
2. Highlight significantly altered pathways
3. Investigate the proximity of amino acid mutations in the same gene
4. Search for gene-based or site-based correlations to mutations and relationships between mutations themselves
5. Correlate mutations to clinical features, using typical correlation measures, and generalized linear models
6. Cross-reference findings with relevant databases such as Pfam, COSMIC, and OMIM

# 软件使用的分析思路

1，生成VCF文件
2，将VCF文件转换成maf（Mutation Annotation Format）文件
3，合并maf文件为一个文件
4，MuSiC bmr calc-covg 生成 **covg** 文件
5，MuSiC bmr calc-bmr 生成 **gene_mrs** 文件
6，MuSiC smg 生成 **significantly mutated genes**
7，Music path-scan 生成 **sm_pathways**

# 安装

```
sudo apt-add-repository "deb http://apt.genome.wustl.edu/ubuntu lucid-genome main"
wget https://apt.genome.wustl.edu/ubuntu/files/genome-institute.asc
sudo apt-key add genome-institute.asc
sudo apt-get update
# fix dependency error Bit::Vector
sudo cpan install Bit::Vector  
sudo apt-get install genome-music
```




# 1，生成VCF文件

可以用varscan2，GATK muTect2等

# 2，将VCF文件转换成maf

参见[前期文章提到的oncotator](http://wp.zxzyl.com/?p=273)，要注意通过设置 --annotate-manual='Tumor_Sample_Barcode:Tumor_sample_name' 设置癌症的样本名（对应第16列）

# 3，合并maf文件 

\# 人懒，这个文件中间有maf的标题栏，没有去掉 ( ° △ °''')︴
`cat *.maf ' grep -v "^#" > myMAF.tsv`

# 4，MuSiC bmr calc-covg 生成 covg 文件

**count covered bases per-gene for each given tumor-normal pair of BAMs.**  

--bam-list	    一个专门记录样本的文件，需要配对的bam(需要先index)，共三列，sample_name（样本名） normal_bam（正常组织bam文件） tumor_bam（肿瘤组织bam文件），每个配对样本的sample_name名称要和第二部设置的名称一致。
格式如下

aaa    /path/to/bam/aaa_normal.bam        /path/to/bam/aaa_tumor.bam
bbb    /path/to/bam/bbb_normal.bam        /path/to/bam/bbb_tumor.bam

--roi-file	    The regions of interest (ROIs) of each gene are typically regions targeted for sequencing or are merged exon loci (from multiple transcripts) of genes with 2-bp flanks (splice junctions).   
roi（基于1 base），可以从  [https://github.com/ding-lab/calc-roi-covg/blob/master/data/ensembl_67_cds_ncrna_and_splice_sites_hg19](https://github.com/ding-lab/calc-roi-covg/blob/master/data/ensembl_67_cds_ncrna_and_splice_sites_hg19) 下载到，格式如下，要注意染色体要与maf对应，比如都有chr三个字符。如果maf中的染色体带chr，可以awk '{print "chr"$0}' old.roi > new.chr.roi 。roi文件中的基因名要和maf中对应。

```
chr1\t11867\t12229\tDDX11L1
chr1\t12611\t12723\tDDX11L1
chr1\t29552\t30041\tMIR1302-11
```




如何生成自己需要的roi文件，过几天我可能会讲。

运行命令

```
genome music bmr calc-covg 
    --bam-list bam_list  
    --output-dir output_dir/   
    --reference-sequence ref.fa  
    --roi-file new.chr.roi 
```




文件夹结构

```
.
├── gene_covgs
│   ├── aaa.covg
│   └── bbb.covg
├── roi_covgs
│   ├── aaa.covg
│   └── bbb.covg
└── total_covgs
2 directories, 5 files
```



# 5，MuSiC bmr calc-bmr 生成 gene_mrs 文件

<!--more-->

**Calculates mutation rates given per-gene coverage (from "music bmr calc-covg"), and a mutation list **

由于music不能识别最新的maf中的突变分类中的部分类型，比如lincRNA等（Unrecognized Variant_Classification "lincRNA" in MAF file ），所以要去掉这些列

```
sed -i '/lincRNA/d' myMAF.tsv
sed -i '/Stop_Codon_Del/d' myMAF.tsv
sed -i '/Start_Codon_Del/d' myMAF.tsv 
sed -i '/Stop_Codon_Ins/d' myMAF.tsv
sed -i '/Start_Codon_SNP/d' myMAF.tsv
sed -i '/Start_Codon_Ins/d' myMAF.tsv
```




output-dir 和--roi-file 参数与上步的设置一致   

运行

```
genome music bmr calc-bmr 
    --bam-list bam_list 
    --maf-file myMAF.tsv  
    --output-dir output_dir/ 
    --reference-sequence ref.fa 
    --roi-file new.chr.roi
```




# 6，MuSiC smg 生成 significantly mutated genes

**Identify significantly mutated genes**

```
genome music smg 
      --gene-mr-file output_dir/gene_mrs 
      --output-file output_dir/smgs
```




结果内容示例如下

```
#Gene   Indels  SNVs    Tot Muts        Covd Bps        Muts pMbp       P-value FCPT    P-value LRT     P-value CT      FDR FCPT        FDR LRT FDR CT
GOLGA6L2        4       22      26      7322    3550.94 0       0       0       0       0       0
GPRIN2  2       27      29      2762    10499.64        0       0       0       0       0       0
KCNJ12  0       40      40      2612    15313.94        0       0       0       0       0       0
KRT18   0       18      18      3050    5901.64 3.10862446895044e-15    0       0       4.50964265930054e-12    0       0
```

# 7，Music path-scan 生成 sm_pathways

**PathScan: a tool for discerning mutational significance in groups of putative cancer genes.**

pathway中的KEGG文件可以从https://github.com/ding-lab/parse-kegg/tree/master/all_pathway_files下载
运行

```
genome music path-scan 
        --bam-list bam_list 
        --gene-covg-dir output_dir/gene_covgs/ 
        --maf-file myMAF.tsv 
        --output-file output_dir/sm_pathways 
        --pathway-file input_dir/pathway_dbs/KEGG.txt    
        --bmr 8.7E-07
```




sm_pathways的结果内容示例如下

```
Pathway Name    Class   Samples_Affected        Total_Variations        p-value FDR
hsa05310        Asthma - Homo sapiens (human)   Human Diseases; Immune System Diseases  2       13      0.88382 1
hsa00062        Fatty acid elongation in mitochondria - Homo sapiens (human)    Metabolism; Lipid Metabolism    2       9       0.92481 0.959873886255924
hsa00130        Ubiquinone and other terpenoid-quinone biosynthesis - Homo sapiens (human)      Metabolism; Metabolism of Cofactors and Vitamins        2       9       0.92689 0.985383058252427
```




# 参考：

[http://gmt.genome.wustl.edu/packages/genome-music/index.html](http://gmt.genome.wustl.edu/packages/genome-music/index.html)

[http://gmt.genome.wustl.edu/packages/genome-music/install.html](http://gmt.genome.wustl.edu/packages/genome-music/install.html)

[https://www.biostars.org/p/95308/](https://www.biostars.org/p/95308/)

[https://github.com/ding-lab/parse-kegg/tree/master/all_pathway_files](https://github.com/ding-lab/parse-kegg/tree/master/all_pathway_files)

\#####################################################################
\#版权所有 转载请告知 版权归作者所有 如有侵权 一经发现 必将追究其法律责任
\#Author: Jason
\####################################################################