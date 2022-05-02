---
title: 预测突变危害的SIFT和PolyPhen2数据库介绍--SIFT and polyphen2 introduction
tags:
  - Mutation
url: archives/728.html
id: 728
categories:
  - Default Category
date: 2016-01-12 13:12:23
---


**SIFT分数介绍**：

SIFT sorts intolerant from tolerant amino acid substitutions ：通过寻找近似的序列，进行比对，计算发生碱基替换的概率，小于0.05被认为是有害的。

SIFT takes a query sequence and uses multiple alignment information to predict tolerated and deleterious substitutions for every position of the query sequence. SIFT is a multistep procedure that (1) searches for similar sequences, (2) chooses closely related sequences that may share similar function to the query sequence , (3) obtains the alignment of these chosen sequences, and (4) calculates normalized probabilities for all possible substitutions from the alignment. Positions with normalized probabilities less than 0.05 are predicted to be deleterious, those greater than or equal to 0.05 are predicted to be tolerated. 

**PolyPhen-2介绍**

考虑结构域，三维结构，通过机器学习然后对突变风险进行预测，计算FPR，。共两组数据集，第一组HumDiv是所有的已知和疾病有关的突变，及所在蛋白在人类和哺乳动物之间的差别，第二组HumVar是已知和疾病有关的突变作为有害和common SNP作为无害共同组成。
HumVar预测具有强烈危害的突变，HumDiv预测可能参与复杂疾病的稀有allele，在HumDiv中，具有中等危害的allele也被归为damaging。
probably damaging的区间值为0.909-1，possibly damaging为0.447-0.908，benign为0-0.446。

Two pairs of datasets were used to train and test PolyPhen-2 prediction models. The first pair, HumDiv, was compiled from all damaging alleles with known effects on the molecular function causing human Mendelian diseases, present in the UniProtKB database, together with differences between human proteins and their closely related mammalian homologs, assumed to be non-damaging. The second pair, HumVar, consisted of all human disease-causing mutations from UniProtKB, together with common human nsSNPs (MAF>1%) without annotated involvement in disease, which were treated as non-damaging.

The user can choose between HumDiv- and HumVar-trained PolyPhen-2 models. Diagnostics of Mendelian diseases requires distinguishing mutations with drastic effects from all the remaining human variation, including abundant mildly deleterious alleles. Thus, HumVar-trained model should be used for this task. In contrast, HumDiv-trained model should be used for evaluating rare alleles at loci potentially involved in complex phenotypes, dense mapping of regions identified by genome-wide association studies, and analysis of natural selection from sequence data, where even mildly deleterious alleles must be treated as damaging.

The authors recommend calling "probably damaging" if the score is between 0.909 and 1, and "possibly damaging" if the score is between 0.447 and 0.908, and "benign" is the score is between 0 and 0.446.（from annovar）

http://genetics.bwh.harvard.edu/pph2/dokuwiki/overview
http://sift.jcvi.org/www/SIFT_help.html