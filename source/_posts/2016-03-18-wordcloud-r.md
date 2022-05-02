---
title: 利用wordcloud R包绘制词云
tags:
  - R
  - wordcloud
url: archives/746.html
id: 746
categories:
  - Default Category
date: 2016-03-18 21:43:39
---



根据词的频率，以词云的形式展示，更加具有表现力。词在'词云'图中字号越大，重要性也就越高。主要涉及数据的挖掘，和数据的展示（可视化）。

![](/wp/f4w/2020/2016-03-18-wordcloud_packages.png)

下面的代码为利用wordcloud包绘制上面词云图

```R
install.packages("wordcloud")
> library(wordcloud)
> mydata mycolors  png("wordcloud_packages.png", width=400,height=400, units='in', res=900)
> wordcloud(mydata$词汇,mydata$词频,random.order=FALSE,random.color=T,colors=mycolors,family="myFont3",min.freq=0)
> dev.off()
```




测试文件下载：[TXT](/wp/f4w/2020/FileAttach/2016-03-18-wordcloud-test.txt)

<!--more-->

有时候，我们得到某会的报告，想知道其中的重点，就需要先利用"分词"技术，将文章正文分成词，统计词出现的频率，绘制词云。出现频率高的词，说明是报告的重点，在词云中展示的比例也较大。如下图。

![](/wp/f4w/2020/2016-03-18-wordcloud-example.png)

同理，如网站的标签云，可以让读者一看对站点的主题有大概了解。同样我们也可以根据基因突变的频率，绘制基因的词云，更具通路中的成员数目绘制通路的词云等等。

\#####################################################################
\#版权所有 转载请告知 版权归作者所有 如有侵权 一经发现 必将追究其法律责任
\#Author: Jason
\####################################################################