---
title: 统计GTF文件中转录本的长度 Calculate transcript length from gtf file
tags:
  - gtf
url: 1067.html
id: 1067
categories:
  - Default Category
date: 2019-12-09 05:37:46
---


gtf 文件INPUT

<pre>chr1    PacBio  exon    763020  763155  .       +       .       gene_id "XLOC_000001"; transcript_id "TCONS_00000001"; exon_number "1"; gene_name "LINC01128"; oId "PB.5.1"; nearest_ref "NR_047519"; class_code "j"; tss_id "TSS1";
chr1    PacBio  exon    764383  764484  .       +       .       gene_id "XLOC_000001"; transcript_id "TCONS_00000001"; exon_number "2"; gene_name "LINC01128"; oId "PB.5.1"; nearest_ref "NR_047519"; class_code "j"; tss_id "TSS1";
chr1    PacBio  exon    776580  776753  .       +       .       gene_id "XLOC_000001"; transcript_id "TCONS_00000001"; exon_number "3"; gene_name "LINC01128"; oId "PB.5.1"; nearest_ref "NR_047519"; class_code "j"; tss_id "TSS1";</pre>

Code

<pre>awk -F"\t" '
{
if ($3=="exon")
    {
        split($9, a, " ");
        ID=a[4]; 
        L[ID]+=$5-$4+1
    } 
}
END{
    for(i in L)
        {print i"\t"L[i]}
    }
' gtf-file >output
</pre>

You can change array index and feature type to choose what you want to count. For example, if you want to calculate gene length, change exon to gene (make sure your gtf file has this feature).

输出OUTPUT
<pre>"TCONS_00052437";       5950
"TCONS_00049398";       988
"TCONS_00031225";       6005
"TCONS_00026369";       825</pre>

参考：https://gist.github.com/sp00nman/10372555

