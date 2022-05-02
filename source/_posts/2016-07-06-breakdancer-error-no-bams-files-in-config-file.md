---
title: 'Breakdancer------Error: no bams files in config file!'
tags:
  - Breakdancer
url: archives/762.html
id: 762
categories:
  - Default Category
date: 2016-07-06 18:49:53
---

breakdancer在call structure variant的时候，生成的文件中只有一行报错的信息 **Error: no bams files in config file!** 

这是因为breakdancer在call SV之前，要先生成配置文件cfg文件。生成cfg文件的依据，是统计bam文件中paired read的插入长度，read的平均长度等信息。如果bam文件中的read都不是配对的或者很少有配对的，在运行bam2cfg.pl时，就会生成空的配置文件，导致检测不出SV，报 **Error: no bams files in config file!** 错误。 

**解决方法：** 

1，准备正确的bam文件，确保足够的配对读长paired reads，以便生成cfg配置文件 

2，同一批样本的插入长度，read平均长度等都差不多，可以将其他文件生成的cfg文件中的 **map:** 选项后改为你的bam文件。即利用其他bam文件生成的cfg文件，当作要检测SV的bam的配置。 

\##################################################################### 
\#版权所有 转载请告知 版权归作者所有 如有侵权 一经发现 必将追究其法律责任 
\#Author: Jason 
\####################################################################