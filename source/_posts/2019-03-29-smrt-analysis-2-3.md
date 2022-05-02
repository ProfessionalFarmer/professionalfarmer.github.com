---
title: 想用smrt analysis-2.3的过来看看
tags:
  - Pacbio
url: archives/1047.html
id: 1047
categories:
  - Default Category
date: 2019-03-29 18:39:05
---

最近找smrt analysis 2.3的程序，真是太辛苦了。我不想用SMRT的图形界面，pacbio又把github上的相关项目obsolete了，tofu项目也没了，pbtranscript装起来各种错误，实在要放弃了，还好看到有人做了2.3的docker镜像。用最近的SMRT6.0中的isoseq3的同学可以忽略本文，isoseq3请移步[https://github.com/PacificBiosciences/IsoSeq3/blob/master/README_v3.1.md](https://github.com/PacificBiosciences/IsoSeq3/blob/master/README_v3.1.md)。

```
docker pull bowhan/smrtanalysis-2.3.0.140936
docker run -it -v /home/bowhan/myData:/data bowhan/smrtanalysis-2.3.0.140936 bash
# -v 挂载目录

#进入smrtshell，有smrtanalysis的环境
/opt/smrtanalysis/current/smrtcmds/bin/smrtshell
# 以iso-seq数据处理为例
# 1. CCS 根据fofn中的h5文件，生成CCS
ConsensusTools.sh CircularConsensus  \
    --minFullPasses 0  --minPredictedAccuracy 75 \
    --parameters /opt/smrtanalysis/install/smrtanalysis_2.3.0.140936/analysis/etc/algorithm_parameters/2014-09/ \
    --numThreads 8 --fofn input.fofn \
    -o /data/output

# 2. classify
pbtranscript.py classify \
    --cpus 8 --min_seq_len 300 \
    --flnc ${prefix}.isoseq_flnc.fasta \
    --nfl ${prefix}.isoseq_nfl.fasta \
    -d ${prefix}.out \
    ${prefix}.ccs.fa \
    ${prefix}.isoseq_draft.fasta 

# 3. cluster
pbtranscript.py cluster \
    isoseq_flnc.fasta final.consensus.fa \
    --nfl_fa isoseq_nfl.fasta -d clusterOut \
    --ccs_fofn reads_of_insert.fofn --bas_fofn input.fofn \
    --cDNA_size under1k --quiver --blasr_nproc 8 \
    --quiver_nproc 8 
```
	
本文转自[https://hub.docker.com/r/bowhan/smrtanalysis-2.3.0.140936/](https://hub.docker.com/r/bowhan/smrtanalysis-2.3.0.140936/)
其他参考：[https://github.com/ben-lerch/IsoSeq-3.0](https://github.com/ben-lerch/IsoSeq-3.0)