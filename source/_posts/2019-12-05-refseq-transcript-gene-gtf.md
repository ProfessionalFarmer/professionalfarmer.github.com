---
title: RefSeq的gtf文件
tags:
  - gtf
url: archives/1065/index.html
id: 1065
categories:
  - Default Category
date: 2019-12-05 04:31:49
---

注释有很多版本，比如ensembl，gencode, ucsc known gene, NCBI的RefSeqGene。最近就需要NM id的注释，但NCBI提供的是gff3格式的，而且很乱。用UCSC table browser下载的gtf版本的RefSeq，没有转录本和基因之间的关系，也没有基因symbol。

比如Ensembl，其实Ensembl的gtf挺好用的，不过这次我因为需要NM编号的注释（笨方法是将ensembl id转成NCBI的refSeq的ID，但这不是最优的方法，ID mapping有可能对不上，不如直接用NM的注释）。

```
chr1    ensembl_havana  gene    11869   14412   .       +       .       gene_id "ENSG00000223972"; gene_version "4"; gene_name "DDX11L1"; gene_source "ensembl_havana"; gene_biotype "pseudogene";
chr1    havana  transcript      11869   14409   .       +       .       gene_id "ENSG00000223972"; gene_version "4"; transcript_id "ENST00000456328"; transcript_version "2"; gene_name "DDX11L1"; gene_source "ensembl_havana"; gene_biotype "pseudogene"; transcript_name "DDX11L1-002"; transcript_source "havana"; transcript_biotype "processed_transcript"; havana_transcript "OTTHUMT00000362751"; havana_transcript_version "1"; tag "basic";
chr1    havana  exon    11869   12227   .       +       .       gene_id "ENSG00000223972"; gene_version "4"; transcript_id "ENST00000456328"; transcript_version "2"; exon_number "1"; gene_name "DDX11L1"; gene_source "ensembl_havana"; gene_biotype "pseudogene"; transcript_name "DDX11L1-002"; transcript_source "havana"; transcript_biotype "processed_transcript"; havana_transcript "OTTHUMT00000362751"; havana_transcript_version "1"; exon_id "ENSE00002234944"; exon_version "1"; tag "basic";
```




UCSC table browser下载的refGene的gtf，这个文件不对的地方是gene id和transcript id是一个，而我需要gene和transcript的关系

```
chr1    hg19_refGene    exon    66999276        66999355        0.000000        +       .       gene_id "NM_001308203"; transcript_id "NM_001308203";
chr1    hg19_refGene    start_codon     67000042        67000044        0.000000        +       .       gene_id "NM_001308203"; transcript_id "NM_001308203";
chr1    hg19_refGene    CDS     67000042        67000051        0.000000        +       0       gene_id "NM_001308203"; transcript_id "NM_001308203";
chr1    hg19_refGene    exon    66999929        67000051        0.000000        +       .       gene_id "NM_001308203"; transcript_id "NM_001308203";
chr1    hg19_refGene    CDS     67091530        67091593        0.000000        +       2       gene_id "NM_001308203"; transcript_id "NM_001308203";
chr1    hg19_refGene    exon    67091530        67091593        0.000000        +       .       gene_id "NM_001308203"; transcript_id "NM_001308203";
```





中间找了很多，终于找到一个方法，https://bioinformatics.stackexchange.com/questions/2548/hg38-gtf-file-with-refseq-annotations

<pre>mysql --user=genome --host=genome-mysql.cse.ucsc.edu -A -N -e "select * from refGene" hg19 ' cut -f2- ' genePredToGtf -source=hg19.refGene.ucsc file stdin stdout > refSeq.hg19.gtf</pre>

genePredToGtf可以从UCSC下载，需要注意的直接下载refFlat的文件（不通过mysql），用genePhredToGtf生成的文件和UCSC table browser下载的gtf文件是一样的，通过mysql下载用genephreadToGtf是我想要的。

比如这样，这才是我想要的

```
chrX    hg19.refGene.ucsc       exon    70683674        70685855        .       +       .       gene_id "TAF1"; transcript_id "NM_138923"; exon_number "38"; exon_id "NM_138923.38"; gene_name "TAF1";
chrX    hg19.refGene.ucsc       CDS     70683674        70683893        .       +       1       gene_id "TAF1"; transcript_id "NM_138923"; exon_number "38"; exon_id "NM_138923.38"; gene_name "TAF1";
chrX    hg19.refGene.ucsc       start_codon     70586225        70586227        .       +       0       gene_id "TAF1"; transcript_id "NM_138923"; exon_number "1"; exon_id "NM_138923.1"; gene_name "TAF1";
chrX    hg19.refGene.ucsc       stop_codon      70683894        70683896        .       +       0       gene_id "TAF1"; transcript_id "NM_138923"; exon_number "38"; exon_id "NM_138923.38"; gene_name "TAF1";
```




Ref: [https://bioinformatics.stackexchange.com/questions/2548/hg38-gtf-file-with-refseq-annotations](https://bioinformatics.stackexchange.com/questions/2548/hg38-gtf-file-with-refseq-annotations)

\#####################################################################
\#版权所有 转载请告知 版权归作者所有 如有侵权 一经发现 必将追究其法律责任
\#Author: Jason
\#####################################################################