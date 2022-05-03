---
title: MobaXterm SSHTunnel/v2ray + Switch Omega + Proxifier
tags:
  - GFW
url: archives/1363/index.html
id: 1363
categories:
  - Default Category
date: 2022-03-29 13:01:20
---


这两年在大陆都是用学校的VPN访问外网，但最近VPN太烂太烂了，经常掉线。这怎么能忍，于是我想到了代理。花钱的事我又不干，我又有VPS，不如让VPS当作代理服务器。一共两种方式都可以实现：socks或v2ray。

# （1）MobaXterm

我一直用mobaXterm的Portabl版本（https://mobaxterm.mobatek.net/），这几年走到哪都会把mobaXterm的文件夹同步过来，避免每次建立新的ssh。我也一直知道MobaXterm有个Tunneling的标签，于是就研究下了MobaXterm自带的。这个比较简单，我直接在mobaxterm上设置后，就建立了隧道。

主要是建立SSH隧道，需要一个境外的ssh帐号。

![](/wp/f4w/2022/2022-03-29-SocksProxy-1.png)

# （2）V2ray

V2ray虽然高级，但是麻烦啊，还要安装还是配置。我参考的是https://www.v2fly.org/，本地用的是v2rayN （https://github.com/2dust/v2rayN）。


无论是1还是2，都是建立和远程代理服务器的连接，然后设定本地localhost的一个特定端口，通过本地的这个端口访问。

# 设置Switch Omega

这个我从会翻墙的时候就在用，不多说，自己设置规则就行。如果你用了v2ray，还可以增加http代理的端口。

![](/wp/f4w/2022/2022-03-29-SocksProxy-2.png)

# 设置Proxifier

设置omega之后，网页可以访问了，但我还想让我电脑的特定软件也翻墙，于是我知道了proxifier，比如我专门让google drive和one drive走外网。本来是想利用windows自带的proxy来设置的，但那和proxifier更好用哈。

![](/wp/f4w/2022/2022-03-29-SocksProxy-3.png)

PS：纪念下从12年就开始用的goagent/xxnet。

#####################################################################
\#版权所有 转载请告知 版权归作者所有 如有侵权 一经发现 必将追究其法律责任
\#Author: Jason
#####################################################################
