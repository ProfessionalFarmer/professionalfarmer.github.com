---
title: How PCR duplicates arise in next-generation sequencing(reprinted)
tags:
  - Sequencing
url: archives/695.html
id: 695
categories:
  - Default Category
date: 2013-03-19 15:49:04
---

PCR duplicates are an everyday annoyance in sequencing.  You spend hundreds or thousands of dollars to get sequencing done, and after you get the reads back, you find that several percent, sometimes even 30% or 70% of your reads are identical copies of each other.  These are called PCR duplicates and most sequencing pipelines recommend removing them or at least marking them (Picard's MarkDuplicates or samtools rmdup are two available tools).<!--more-->

Ever since I got into sequencing I wanted to know how these duplicates arise - what does it mean for a read to be a PCR duplicate and why do we ignore them?  I've Googled this over and over and never found a satisfying explanation.  So after hearing Shawn Levy give an excellent introduction to the biochemistry and technology of sequencing at the first day of the UAB sequencing course, I asked him how PCR duplicates arise in next-generation sequencing.  In this post I'll explain the answer he gave me.

First, let's put this in context of the basic steps of library prep and sequencing:

Shatter genomic DNA, e.g. with a sonicator.
Ligate adapters to both ends of the fragments.
PCR amplify the fragments with adapters
Create an oil-water emulsion of micrometer beads and DNA molecules (for Roche or Ion Torrent technologies) or spread DNA molecules across flowcells (for Illumina technology).  Goal is to get exactly one DNA molecule per bead or per flowcell lawn of primers.  This depends purely on probability, based on the concentration of DNA.
Use bridge PCR to amplify the single molecule on each bead or each lawn so that you can get a strong enough signal (whether light or pH) to detect.  Usually this requires several hundred or low thousands of molecules.
Sequence by synthesis of complementary strand: pyrosequencing  (Roche),reversible terminator chemistry (Illumina), or ion semiconductor (Ion Torrent).

PCR duplicates arise in step 3.  In step 3 you are intentionally creating multiple copies of each original genomic DNA molecule so that you have enough of them, therefore someamount of PCR duplication is inevitable.  PCR duplicates occur when two copies of the same original molecule get onto different beads or different primer lawns in a flowcell.  Ideally in step 3 you are amplifying only ~64-fold (Shawn Levy said he prefers to do no more than 6 rounds of PCR, hence 26) and so the library still has high "complexity", i.e. information entropy.  This will let you have the fraction of your final reads that are PCR duplicates can be as low as 4%.  Higher rates of PCR duplicates e.g. 30% arise when people have too little starting material such that greater amplification of the library is needed in step 3, or when people have too great a variance in fragment size, such that smaller fragments, which are easier to PCR amplify, end up over-represented.

[http://www.cureffi.org/2012/12/11/how-pcr-duplicates-arise-in-next-generation-sequencing](http://www.cureffi.org/2012/12/11/how-pcr-duplicates-arise-in-next-generation-sequencing)