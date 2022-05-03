---
title: 单细胞测序技术及应用进展-Single Cell Sequencing Technology and Its Applications Progress
tags:
  - Sequencing
url: archives/711/index.html
id: 711
categories:
  - Default Category
date: 2015-05-05 21:19:31
---

<span style="color:#ff0000;">**如有引用和转载，请告知。**</span>

同一组织中的细胞往往被认为是具有相同状态的功能单位，传统的检测手段分析的是细胞群体的总体平均反应。然而通过对单个细胞的DNA或RNA进行测序，表明组织系统层面的功能是由异质性细胞构成。单细胞测序以单个细胞为单位，通过全基因组或转录组扩增，进行高通量测序，能够揭示单个细胞的基因结构和基因表达状态，反映细胞间的异质性，在肿瘤、发育生物学、微生物学、神经科学等领域发挥重要作用，正成为生命科学研究的焦点。单细胞测序的难点是单个细胞的分离、单细胞基因组和转录组的扩增。本文主要介绍和分析了单细胞测序技术中常用的单细胞分离技术、单细胞基因组扩增技术和转录组扩增技术及其优缺点，并对当前已经取得成果的应用领域进行了阐述，为单细胞测序技术的研究与应用提供参考。
关键词：单细胞；分离；扩增；应用

Individual cells of the same phenotype are commonly viewed as identical functional units of a tissue. The analysis of traditional detection method always bases on the overall average reaction of cells. However, the sequencing of DNA or RNA from single cells suggests the system-level function of a tissue is produced by heterogeneous cell. Single cell genome or transcriptome can be sequenced after amplification based on single cell sequencing. It can reveal the structure and expression of genes and the heterogeneity between cells. Single cell sequencing technology has come into focus for the achievements in cancer, developmental biology, microbiology and neuroscience. The difficulty involves in single cell isolation, whole genome amplification and transcriptome amplification. In this review, we summarize the common single cell isolation technology, whole genome amplification technology and transcriptome amplification technology, and analyze the advantages and disadvantages of current technologies. We also introduce the successful applications in different fields. This review provides references of single cell sequencing study and application.
Key words：Single cell; Isolation; Amplification; Application<!--more-->

<span style="color:#ff0000;">**如有引用和转载，请告知。**</span>

在过去的十年里，随着测序技术水平的改进，测序通量在不断提高，测序成本的下降更是快于摩尔定律。大规模测序平台可以同时对数以万计的DNA分子同时测序，有助于快速和准确地获取生物体的遗传信息，使得研究人员以更低的成本，更加全面深入地分析全基因组、转录组、甲基化组等各项组学数据(Shendure and Ji，2008)。这完全改变了过去的研究模式，给生命科学领域带来了翻天覆地的变化(Mardis，2008)。

细胞是生命的单位，然而大多数的人类基因组、癌症或其他研究仍然是通过从多个细胞中抽提DNA来进行测序，这忽略了细胞间的差异对于控制基因表达、细胞行为的影响，实验结果往往表示的是细胞群体中信号表达的均值，或者只代表其中在数量上占优势的细胞信息，单个细胞独有的细胞特性往往被忽略。有研究表明，样本中单个细胞之间的基因表达调控也存在差异(Rosenfeld et al.，2005)。传统高通量测序方法，难以应用在对自然界中难以培养的微生物的研究、罕见循环肿瘤细胞的转录组分析、人胚胎发生最早期的分化特征研究、肿瘤的非均质性和微进化研究等领域(Ramsköld et al.，2012)。随着测序、细胞分离和全基因组扩增技术的发展，在单个细胞水平上对基因组进行测序的单细胞测序技术能够解决上述局限性。2009年，Tang等通过改进先前用于微阵列分析的单细胞转录组扩增方法，分析了来自小鼠四细胞胚胎阶段的单个卵裂球的转录组(Tang et al.，2009)。2011年，Navin通过流式细胞分离，对200个癌细胞分别进行测序，研究癌症的进化(Navin et al.，2011)，同年《自然方法》杂志(Nature Methods)将单细胞研究方法列为未来几年最值得关注的技术领域之一(de Souza，2012)。2013年，《科学》杂志(Science)将单细胞测序列为年度最值得关注的六大领域榜首，《自然方法》杂志将单细胞测序的应用列为2013年年度最重要的方法学进展(Pennisi，2012；Chi，2014)。单细胞测序技术能够解析细胞间更加细微的差异，推动微生物、发育生物学、神经科学、免疫、癌症等领域的发展，正在成为生命科学研究的焦点(Blainey，2013；Chi，2014)。本文从单细胞测序基本路线和技术应用两方面对单细胞测序技术的最近研究进展进行了阐述。

## 1 单细胞分离技术

单细胞测序的第一步是将目的细胞的从样本中分离出。一些单细胞分离方法已经被开发出来，目前主要的技术包括梯度稀释法(Serial dilution)(Zhang et al.，2006；Reizel et al.，2011)、显微操作技术(Micromanipulation)(Kvist et al.，2007)、荧光激活细胞分选(Fluorescence activated cell sorting, FACS)(Stepanauskas and Sieracki，2007)、微流控技术(Microfluidics)(Marcy et al.，2007) 和激光捕获显微切割(Laser capture microdissection，LCM)(Frumkin et al.，2008；Yachida et al.，2010)。

荧光激活细胞分选技术借助流式细胞仪，用激光束激发单行流动的与荧光素标记抗体相结合的细胞，根据激发的荧光信号对细胞进行分选，是现在最常用的单细胞分离技术。Navin等基于流式细胞仪的FACS法，根据肿瘤细胞的DNA含量进行筛选，并将单个细胞准确置于96孔板(Navin et al.，2011)。FACS法可以依据细胞的多个特征（比如大小，粒度，内外荧光等）进行快速分离(Yilmaz and Singh，2012)。FACS的优势是高准确度、高灵敏度和高通量，虽然过程复杂，但此实验技术成熟，有统一的标准。缺点是FACS需要大量的悬浮细胞作为原始材料，可能影响低丰度细胞亚群的产出，此外仪器中快速流动的液流可能会对细胞的活性和状态产生一定的影响(Shapiro et al.，2013)。

显微操作技术是利用显微操作仪，直接实现单个细胞的分离，是一种强大灵活的获取单个细胞的技术。例如，从土壤中分离无法人工培养的微生物(Kvist et al.，2007)，从白蚁肠道中分离共生体(Sato et al.，2009)，分离胚胎期的内细胞团或者单个胚胎干细胞(Tang et al.，2006)。显微操作也是常用的单细胞分离方法，典型的显微控制系统包含一个倒置显微镜加上一个操纵杆操作,电动精密控制平台。其优点是操作容易进行，通过可视化界面直观地分离单个细胞，并且成本低，主要用于较小细胞群体中的目标细胞分离。缺点是通量低，分离过程中容易损伤细胞，细胞识别的过程中容易出错(Shapiro et al.，2013)。半自动化的细胞分离设备的研发，可以克服上述的部分不足(Choi et al.，2010)。

梯度稀释法是通过将细胞进行梯度稀释，最终得到单个细胞。其优点是技术简单、成本低廉、适用于样本可以培养的研究中，比如分离单个大肠杆菌和原绿球藻进行基因组测序(Zhang et al.，2006)；缺点是在分离过程中容易出现分离错误或者丢失细胞。微流控技术是在微米级通道内分离、捕获单个细胞(Marcy et al.，2007)，北京大学生命科学学院的研究人员便通过微流控芯片实现单细胞转录组测序, 大大减少了试剂用量，在反应效率得到提升的同时极大地抑制了污染的发生，还减少了操作误差，实现了更高的可靠性和更好的平行性(Streets et al.，2014)。激光捕获显微切割是在不破坏组织结构、保存要捕获的细胞、保证其周围组织形态完整的前提下，直接从冰冻或石蜡包埋组织切片中精确地分离单个的细胞(Bonner et al.，1997)，大多用在与人类健康相关的单细胞基因组学研究中(Frumkin et al.，2008)。该技术的缺点是，花费高、切割不精确，可能丢失细胞核遗传物质(Yilmaz and Singh，2012)。

## 2 单细胞全基因组扩增技术

单细胞全基因组扩增(Whole Genome Amplification, WGA)其原理是通过将单个细胞溶解得到微量基因组DNA进行高效地扩增，获得高覆盖度的单细胞基因组的技术。 Roger等最早对一个细胞DNA进行扩增并测序(Raghunathan et al.，2005)。准确的获取单个细胞遗传信息的前提是获得高覆盖率的基因组，然后才能进行下一步测序。

基于热循环以PCR为基础的全基因组扩增技术，有简并寡核苷酸引物PCR技术 (degenerate oligonucleotide primed PCR, DOP-PCR)(Navin et al.，2011) 、连接反应介导的PCR 技术(ligation mediated PRC, LM-PCR)(Cheung and Nelson，1996)、扩增前引物延伸反应技术(primer extension pre-amplification, PEP)。这些技术，是早期常用的经典技术，但PCR过程中，DNA片段的大小、DNA的二级结构、GC含量等会影响聚合酶的扩增效率甚至导致酶滑链或者从模板上脱离，不能完整地覆盖基因组，并且会往序列中引入很多错误和非特异性扩增产物，存在扩增偏倚(amplification bias)(Viguera et al.，2001；Dean et al.，2002；Zong et al.，2012)。不同基因组位置的扩增效率和错误，对下一步的分析是一种挑战(Li et al.，2008)。

现在最新的技术是基于等温反应但不以PCR为基础的全基因组扩增技术，例如有多重置换扩增技术(multiple displacement amplification, MDA)(Raghunathan et al.，2005)，基于引物酶的全基因组扩增技术(primase-based Whole Genome Amplification, pWGA)(Li et al.，2008)等。MDA技术是在恒温下利用具有强模板结合的phi29DNA聚合酶和六聚物进行链置换扩增反应。近期，其优点是样本无需纯化，操作简单，产生的DNA片段长（10-100kb），错误率低，有着良好的DNA扩增覆盖效果，扩增出10-100kb大小的片段(Raghunathan et al.，2005)，是比较常用的技术，缺点是起始模板量低时扩增偏差性大(Zong et al.，2012)。华中农大克服了植物细胞壁的障碍，使用MDA技术，实现玉米单细胞测序，首次证实了在植物中存在较强的重组负干涉和复杂的染色单体干涉、环境因素显著影响重组频率等重要遗传学现象(Li et al.，2015)。pWGA技术基于T7噬菌体在体细胞中进行DNA复制的原理，利用gp4引物酶合成引物，在体外再造T7噬菌体DNA复制过程的等温反应。其优点是不需要外源引物，避免引物导致的复制偏差，扩增效率和产量高，要求的起始模板量低，但保真性稍差。

为了提高扩增的覆盖度和均匀度，相关技术也在不断发明和改进。Xie等发明了基于多次退火环状循环的扩增技术(multiple annealing and looping-based amplification cycles, MALBAC)，结合MDA扩增技术和PCR扩增技术的优势，通过利用特殊设计的引物，巧妙地使扩增子的结尾通过互补而成环，进而在一定程度上防止了基因组DNA的指数性扩增，明显降低了扩增偏倚性，并显著提高覆盖度(Zong et al.，2012)。需要注意的是，不同的扩增技术，适用于不同的实验分析和测序技术。

## 3 单细胞转录组扩增技术

单细胞转录组扩增，需要通过PCR将mRNA逆转录成cDNA。mRNA在细胞内的拷贝数目要多于DNA，单细胞转录组扩增的关键在于如何高效、低偏倚地将mRNA逆转录并形成双链DNA(Xue et al.，2015)。有的方法是对整个转录子进行测序，有的方法只对转录子的5'和3'端进行测序。但不论采用何种方法，目的都是捕获原始的RNA分子，然后均一的、准确的对其进行扩增。大多数扩增技术，都要考虑往cDNA中引入上下游引物结合位点，以便通过PCR扩增。

Tang等首次基于微阵列分析的方法实现了单细胞RNA测序，通过多聚T碱基作引物，逆转录合成第一条cDNA并延长到3kb，并在3'末端添加多聚A碱基，以此作为合成第二条cDNA链时多聚T碱基引物的结合位点，接下来通过PCR对cDNA进行扩增(Tang et al.，2009)。最终发现了以往芯片未能检测到的基因和可变剪切位点。但是基于芯片的技术比较封闭，不能检测分析未知的基因，不能确定mRNA的具体长度和序列，无法区分正反义链上的转录本。

SMART则是目前常用的一种mRNA全长扩增技术。该技术依然用多聚T碱基作下游引物开始逆转录，但使用的逆转录酶是SMARTscibeRT酶，会在转录的末端延长出几个超过模板的C碱基，转录出的cDNA可以用带3个G碱基的上游引物进行扩增(Ramsköld et al.，2012)。Sandberg等通过这项技术，研究分析了复发性恶性黑色素瘤病人的肿瘤细胞的基因表达情况，证实肿瘤细胞能够激活很多负责躲避体内监控系统的膜蛋白。随后，Sandberg研究小组改进了初始方法，提高了捕获RNA分子的数量，获得更加完整的基因序列，并命名为SMART-seq2技术。SMART-seq2利用现成的试剂，因此成本比较低。STRT(single-cell tagged reverse transcription, STRT)技术则利用生物素将cDNA固定在磁珠上，并引入阅读标记(Islam et al.，2011)。SMART技术不稳定，低水平表达的转录组可能丢失。Phi29聚合酶扩增技术(Phi29-mRNA amplification，PMA)利用全基因组扩增技术中用到的Phi29DNA聚合酶的链置换和连续合成特性，对环化的cDNA进行高效扩增；SMA(semirandom primed PCR-based mRNA transcriptome amplification)技术则利用带有发卡结构的寡核苷酸作引物(Pan et al.，2013)。这些技术都可以获得mRNA的全长信息，但最低起始量、检测灵敏度、稳定性不尽相同，使用的研究范围也不一致。

随着技术的不断发展，单个细胞转录组扩增技术中普遍存在的低覆盖率的弊端和单细胞中除mRNA外其他非编码RNA难以检测分析的缺陷等都会被改进和优化。

## 4单细胞测序的应用进展

### 4.1单细胞测序在肿瘤研究中的应用
癌症细胞研究是单细胞测序首先应用的领域。Navin等应用单细胞测序技术对来自两个人类乳腺癌病例的各100个单细胞进行测序分析肿瘤群体结构和进化，证实其中一种异质性肿瘤存在三种截然不同的细胞亚群，而另一种是由一群遗传上相同的细胞构成(Navin et al.，2011)。他们的数据也表明肿瘤生长是由少量持久中间体和克隆扩增导致的。Xu等对肾肿瘤进行单细胞测序，发现没有明显的细胞亚群，肿瘤细胞之间的突变频率和位置也不尽相同，表明肾肿瘤更加具有异质性，需要开发更加有效的细胞靶向疗法(Xu et al.，2012)。这样也有利于研究肿瘤的发展机制和转移机制。Ramsköld等运用SMART-Seq技术，发现经过单个细胞测序会提高测量基因表达值时的噪音，但通过分析不同细胞类型中微量的个体细胞表达情况，依然可以鉴别出许多差异表达基因，发现了循环系统肿瘤细胞中的活跃基因，并发现了不同的表达模式和候选标记(Ramsköld et al.，2012)。Felthaus等通过对口腔鳞状细胞癌的干细胞进行分析，发现口腔鳞状细胞癌对常规放化疗的抵抗可能由肿瘤的干细胞导致(Felthaus et al.，2011)。

### 4.2单细胞测序在发育生物学中的应用
单细胞测序使得通过单个细胞研究个体发育成为可能。Xue等分别对人和小鼠胚胎从卵母细胞到桑椹胚进行单细胞转录组测序分析。通过加权基因共表达网络分析，发现每个发育阶段都可以被少量由共表达基因组成的功能模块准确区分，表明从分裂到桑椹胚阶段中细胞循环、基因调控、翻译和代谢中的转录谱以一定的顺序变化着，此外也研究了人和小鼠胚胎发育过程中基因表达情况的差异(Xue et al.，2013)。Wang等人应用微流控系统对一个人的91个生殖细胞进行单细胞全基因组高通量测序，将得到的高密度基因分型结果绘制了个人水平的染色体重组图，来观测个体生殖细胞基因组的多样性，发现在低分辨率情况下结果与种群数据一致，但高分辨率下表现出不同，这些差异表明个体特征可能在群体范围内被稀释(Zong et al.，2012)。Tang通过单细胞转录组测序，研究体外胚胎内团细胞向胚胎干细胞转化的发生机制，发现了包括新陈代谢基因在内的分子和转录本可变剪切发生了显著变化，有助于研究疾病组织中成熟细胞的转变发生机制(Tang et al.，2010)。

### 4.3单细胞测序在微生物研究中的应用
单细胞测序使得微生物研究得到发展。传统的测序方法无法对自然界中难以培养的微生物进行测序，单细胞测序则区别于宏基因组研究，可以对单个微生物细胞进行，进而可以发现新的微生物，构建新的微生物进化树和微生物基因组序列，加深科学家对微生物生命活动过程的研究和理解(Lasken，2007；Blainey，2013)。Mußmann等对一个不能人为培养的海洋微生物进行测序分析，发现一种新的硫化细菌，得到接近70%的基因组草图，平均重叠群长度为1kb，预测出的基因有相当大的比例被鉴定为硫氧化、氧化呼吸、二氧化碳固定过程中的关键酶，并发现可能利用无机硫化物和二甲基亚砜作为电子受体(Mußmann et al.，2007)。Brauer等也对一个海洋微生物进行了测序，生成了单细胞基因组序列，通过对16SrRNA序列进化分析发现与硫氧化有关，发现了参与有氧代谢有关的基因(Brauer，2012)。新基因的发现有助于研究人员对微生物分类、进化和生命活动的探索。

### 4.4单细胞测序在神经科学中的应用
最近，科学家开始用单细胞测序研究神经元细胞(Chi，2014)。Muotri等通过单细胞测序研究长散在核元件(long interspersed nuclear elements, LINEs)与神经元的关系。发现在神经元干细胞向干细胞分化的过程中，长散在核元件会通过反转录转座在基因组内发生跳跃形成新的插入，而且每个神经元可能含有独特的长散在核元件插入（平均每个细胞有80到300个插入），也就是说每个神经元可能不同于其他的神经元，这些差异可能影响个体对神经疾病的易感性(Coufal et al.，2009)。McConnell等从三个正常人的脑中取了110个额叶皮质神经细胞进行分析，发现相当大比例的神经细胞都含有大的拷贝数变异(CNV)，从正常人皮肤细胞诱导分化成的神经元含有的拷贝数变异也大于正常的皮肤细胞(McConnell et al.，2013)。这表明来自诱导性多潜能干细胞的神经元也可能适合对细胞异质性功能影响的研究。这些都可以用来研究异质性细胞群体的基因组多样性。Gole也通过单细胞测序发现人的神经细胞至少有一个区域含有百万碱基水平的单拷贝变异(Gole et al.，2013)。

## 5展望
当前，单细胞测序已经在肿瘤、发育生物学、神经科学、微生物等领域取得了丰富的成果。在单细胞层面，肿瘤组织和分化中的胚胎干细胞甚至正常组织中都表现出异质性。单细胞研究可能帮助研究人员更好的研究理解为什么有些细胞会退化而相邻的细胞却表现正常，为什么有些细胞会对药物产生反应而其他细胞没有。单细胞测序或许可以发现更多类型的细胞，研究发育过程中细胞的分化，研究组织中的细胞之间如何协同工作，甚至鉴别出在癌症或者疾病早期起作用的关键细胞。随着更多微生物的鉴定及其基因组的拼接和功能基因的发现，将更加丰富人类对自然界多样性和生物进化的认识。

此外，单细胞甲基化组和蛋白质组等组学分析技术也会推动生命科学的进一步发展。基于甲基化敏感性显著性内切酶的单细胞甲基化率检测方法RSMA(enzyme-based single cell methylation assay)技术，可以用来检测单个癌细胞之间的甲基化差异(Kantlehner et al.，2011)。单细胞DNA甲基化分析技术，也可以寻找胚胎中的分子改变，检测人类胚胎的基因缺陷(Lorthongpanich et al.，2013)。结合单细胞转录组测序和基因组分析技术，未来可以分析复杂疾病中印记基因的异常表达调控机制，为疾病诊断提供依据；研究干细胞和癌症分化过程中甲基化调控和蛋白质变化规律，揭示传统生命科学研究中未能探索的奥秘。

但目前单细胞测序还存在着问题，比如扩增存在偏倚性，非特异性扩增，建库过程中存在污染，检测灵敏度不高，技术噪音高，操作失误率高，重复性差、除mRNA以外的非编码RNA难以检测等等。这些问题的存在，使下一步的数据分析变得困难，目前很少有专门针对单细胞测序数据分析的软件和工具。未来几年，相信随着高通量技术、细胞分离技术、基因组转录组扩增技术的发展，扩增的覆盖度和灵敏度都将会提高，同时单细胞测序的通量会提升、成本也会下降，针对单细胞测序的数据分析工具和软件也会更强大。单细胞测序技术的研究和检测会更加细致深入，应用领域也会越来越广，并且会从基础研究扩展到实际应用，比如产前诊断，疾病治疗(Hou et al.，2013)。

随着单细胞测序技术的发展，在单个细胞水平探讨生命过程一定是未来的研究热点，生命科学研究人员会以全新的视角探究生命活动规律，造福人类健康和农业生产。

## 参考文献

Blainey P. C., 2013, The future is now: single-cell genomics of bacteria and archaea, FEMS microbiology reviews, 37(3): 407-427.

Bonner R. F., Emmert-Buck M., Cole K., Pohida T., Chuaqui R., Goldstein S. ， Liotta L. A., 1997, Laser capture microdissection: molecular analysis of tissue, Science (New York, NY), 278(5342): 1481, 1483.

Brauer S., 2012, Ubiquitous dissolved inorganic carbon assimilation by marine bacteria in the Pacific Northwest coastal ocean as determined by stable isotope probing.

Cheung V. G., and Nelson S. F., 1996, Whole genome amplification using a degenerate oligonucleotide primer allows hundreds of genotypes to be performed on less than one nanogram of genomic DNA, Proceedings of the National Academy of Sciences, 93(25): 14676-14679.

Chi K. R., 2014, Singled out for sequencing, Nature methods, 11(1): 13-17.

Choi J. H., Ogunniyi A. O., Du M., Du M., Kretschmann M., Eberhardt J., and Love J. C., 2010, Development and optimization of a process for automated recovery of single cells identified by microengraving, Biotechnology progress, 26(3): 888-895.

Coufal N. G., Garcia-Perez J. L., Peng G. E., Yeo G. W., Mu Y., Lovci M. T., Morell M., O'Shea K. S., Moran J. V., and Gage F. H., 2009, L1 retrotransposition in human neural progenitor cells, Nature, 460(7259): 1127-1131.

de Souza N., 2012, Single-cell methods, Nature Methods, 9(1): 35-35.

Dean F. B., Hosono S., Fang L., Wu X., Faruqi A. F., Bray-Ward P., Sun Z., Zong Q., Du Y. and Du J., 2002, Comprehensive human genome amplification using multiple displacement amplification, Proceedings of the National Academy of Sciences, 99(8): 5261-5266.

Felthaus O., Ettl T., Gosau M., Driemel O., Brockhoff G., Reck A., Zeitler K., Hautmann M., Reichert T. E., and Schmalz G., 2011, Cancer stem cell-like cells from a single cell of oral squamous carcinoma cell lines, Biochemical and biophysical research communications, 407(1): 28-33.

Frumkin D., Wasserstrom A., Itzkovitz S., Harmelin A., Rechavi G., and Shapiro E., 2008, Amplification of multiple genomic loci from single cells isolated by laser micro-dissection of tissues, BMC biotechnology, 8(1): 17.

Gole J., Gore A., Richards A., Chiu Y.-J., Fung H.-L., Bushman D., Chiang H.-I., Chun J., Lo Y.-H., and Zhang K., 2013, Massively parallel polymerase cloning and genome sequencing of single cells using nanoliter microwells, Nature biotechnology, 31(12): 1126-1132.

Hou Y., Fan W., Yan L., Li R., Lian Y., Huang J., Li J., Xu L., Tang F., and Xie X. S., 2013, Genome analyses of single human oocytes, Cell, 155(7): 1492-1506.

Islam S., Kjällquist U., Moliner A., Zajac P., Fan J.-B., Lönnerberg P., and Linnarsson S., 2011, Characterization of the single-cell transcriptional landscape by highly multiplex RNA-seq, Genome research, 21(7): 1160-1167.

Kantlehner M., Kirchner R., Hartmann P., Ellwart J. W., Alunni-Fabbroni M., and Schumacher A., 2011, A high-throughput DNA methylation analysis of a single cell, Nucleic acids research: gkq1357.

Kvist T., Ahring B. K., Lasken R. S., and Westermann P., 2007, Specific single-cell isolation and genomic amplification of uncultured microorganisms, Applied microbiology and biotechnology, 74(4): 926-935.

Lasken R. S., 2007, Single-cell genomic sequencing using multiple displacement amplification, Current opinion in microbiology, 10(5): 510-516.

Li X., Li L., and Yan J., 2015, Dissecting meiotic recombination based on tetrad analysis by single-microspore sequencing in maize, Nature communications, 6.

Li Y., Kim H.-J., Zheng C., Chow W. H. A., Lim J., Keenan B., Pan X., Lemieux B., and Kong H., 2008, Primase-based whole genome amplification, Nucleic acids research, 36(13): e79-e79.

Lorthongpanich C., Cheow L. F., Balu S., Quake S. R., Knowles B. B., Burkholder W. F., Solter D., and Messerschmidt D. M., 2013, Single-cell DNA-methylation analysis reveals epigenetic chimerism in preimplantation embryos, Science, 341(6150): 1110-1112.

Marcy Y., Ishoey T., Lasken R. S., Stockwell T. B., Walenz B. P., Halpern A. L., Beeson K. Y., Goldberg S. M. D., and Quake S. R., 2007, Nanoliter reactors improve multiple displacement amplification of genomes from single cells, PLoS genetics, 3(9): e155.

Mardis E. R., 2008, The impact of next-generation sequencing technology on genetics, Trends in genetics, 24(3): 133.

McConnell M. J., Lindberg M. R., Brennand K. J., Piper J. C., Voet T., Cowing-Zitron C., Shumilina S., Lasken R. S., Vermeesch J. R., and Hall I. M., 2013, Mosaic copy number variation in human neurons, Science, 342(6158): 632-637.

Mußmann M., Hu F. Z., Richter M., de Beer D., Preisler A., Jørgensen B. B., Huntemann M., Glöckner F. O., Amann R., and Koopman W. J. H., 2007, Insights into the genome of large sulfur bacteria revealed by analysis of single filaments, PLoS biology, 5(9): e230.

Navin N., Kendall J., Troge J., Andrews P., Rodgers L., McIndoo J., Cook K., Stepansky A., Levy D., and Esposito D., 2011, Tumour evolution inferred by single-cell sequencing, Nature, 472(7341): 90-94.

Pan X., Durrett R. E., Zhu H., Tanaka Y., Li Y., Zi X., Marjani S. L., Euskirchen G., Ma C., and LaMotte R. H., 2013, Two methods for full-length RNA sequencing for low quantities of cells and single cells, Proceedings of the National Academy of Sciences, 110(2): 594-599.

Pennisi E., 2012, Single-Cell Sequencing Tackles Basic and Biomedical Questions, Science, 336(6084): 976-977.

Raghunathan A., Ferguson H. R., Bornarth C. J., Song W., Driscoll M., and Lasken R. S., 2005, Genomic DNA amplification from a single bacterium, Applied and environmental microbiology, 71(6): 3342-3347.

Ramsköld D., Luo S., Wang Y.-C., Li R., Deng Q., Faridani O. R., Daniels G. A., Khrebtukova I., Loring J. F., and Laurent L. C., 2012, Full-length mRNA-Seq from single-cell levels of RNA and individual circulating tumor cells, Nature biotechnology, 30(8): 777-782.

Reizel Y., Chapal-Ilani N., Adar R., Itzkovitz S., Elbaz J., Maruvka Y. E., Segev E., Shlush L. I., Dekel N., and Shapiro E., 2011, Colon stem cell and crypt dynamics exposed by cell lineage reconstruction, PLoS genetics, 7(7): e1002192.

Rosenfeld N., Young J. W., Alon U., Swain P. S., and Elowitz M. B., 2005, Gene regulation at the single-cell level, Science, 307(5717): 1962-1965.

Sato T., Hongoh Y., Noda S., Hattori S., Ui S., and Ohkuma M., 2009, Candidatus Desulfovibrio trichonymphae, a novel intracellular symbiont of the flagellate Trichonympha agilis in termite gut, Environmental microbiology, 11(4): 1007-1015.

Shapiro E., Biezuner T., and Linnarsson S., 2013, Single-cell sequencing-based technologies will revolutionize whole-organism science, Nature Reviews Genetics, 14(9): 618-630.

Shendure J., and Ji H., 2008, Next-generation DNA sequencing, Nature biotechnology, 26(10): 1135-1145.

Stepanauskas R., and Sieracki M. E., 2007, Matching phylogeny and metabolism in the uncultured marine bacteria, one cell at a time, Proceedings of the National Academy of Sciences, 104(21): 9052-9057.

Streets A. M., Zhang X., Cao C., Pang Y., Wu X., Xiong L., Yang L., Fu Y., Zhao L., and Tang F., 2014, Microfluidic single-cell whole-transcriptome sequencing, Proceedings of the National Academy of Sciences, 111(19): 7048-7053.

Tang F., Barbacioru C., Bao S., Lee C., Nordman E., Wang X., Lao K., and Surani M. A., 2010, Tracing the derivation of embryonic stem cells from the inner cell mass by single-cell RNA-Seq analysis, Cell stem cell, 6(5): 468-478.

Tang F., Barbacioru C., Wang Y., Nordman E., Lee C., Xu N., Wang X., Bodeau J., Tuch B. B., and Siddiqui A., 2009, mRNA-Seq whole-transcriptome analysis of a single cell, Nature methods, 6(5): 377-382.

Tang F., Hajkova P., Barton S. C., O'Carroll D., Lee C., Lao K., and Surani M. A., 2006, 220-plex microRNA expression profile of a single cell, Nature protocols, 1(3): 1154-1159.

Viguera E., Canceill D., and Ehrlich S. D., 2001, Replication slippage involves DNA polymerase pausing and dissociation, The EMBO journal, 20(10): 2587-2595.

Xu X., Hou Y., Yin X., Bao L., Tang A., Song L., Li F., Tsang S., Wu K., and Wu H., 2012, Single-cell exome sequencing reveals single-nucleotide mutation characteristics of a kidney tumor, Cell, 148(5): 886-895.

Xue R., Li R., and Bai F., 2015, Single cell sequencing: technique, application, and future development, Science Bulletin, 60(1): 33-42.

Xue Z., Huang K., Cai C., Cai L., Jiang C.-y., Feng Y., Liu Z., Zeng Q., Cheng L., and Sun Y. E., 2013, Genetic programs in human and mouse early embryos revealed by single-cell RNA [thinsp] sequencing, Nature, 500(7464): 593-597.

Yachida S., Jones S., Bozic I., Antal T., Leary R., Fu B., Kamiyama M., Hruban R. H., Eshleman J. R., and Nowak M. A., 2010, Distant metastasis occurs late during the genetic evolution of pancreatic cancer, Nature, 467(7319): 1114-1117.

Yilmaz S., and Singh A. K., 2012, Single cell genome sequencing, Current opinion in biotechnology, 23(3): 437-443.

Zhang K., Martiny A. C., Reppas N. B., Barry K. W., Malek J., Chisholm S. W., and Church G. M., 2006, Sequencing genomes from single cells by polymerase cloning, Nature biotechnology, 24(6): 680-686.

Zong C., Lu S., Chapman A. R., and Xie X. S., 2012, Genome-wide detection of single-nucleotide and copy-number variations of a single human cell, Science, 338(6114): 1622-1626.