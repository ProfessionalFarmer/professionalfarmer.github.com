---
title: 在Mac上安装cirocs，在Mac上安装perl GD模块
tags:
  - cirocs
  - Mac
url: archives/712/index.html
id: 712
categories:
  - Default Category
date: 2015-05-08 08:38:25
---

久闻Circos作图高大上，今天一师兄让我帮他用circos画个图，便试着在Mac安装Circos。Circos是作图软件，需要GD Graphics库，关于如何在Mac上用perl安装GD，可以直接看两行星号之间的内容。
<!--more-->

下载压缩包之后
`tar xvfz circos-***.tgz`

我不喜欢乱将软件软连接到环境变量的路径中，所以直奔主题
`$ cd circos-0.67-7/bin/
circos-0.67-7/bin$ ./circos
`
报错没有找到env
`-bash: ./circos: /bin/env: bad interpreter: No such file or directory`

执行
```
circos-0.67-7/bin$ which env
/usr/bin/env
```

将circos-0.67-7/bin/circos文件中的第一行

```
#! /bin/env perl替换为
#!/usr/bin/env perl
```

运行,虽然Mac 的OSX 系统自带peril，但依然提示我有错，缺少perl的组件
```
circos-0.67-7/bin$ ./circos
*** REQUIRED MODULE(S) MISSING OR OUT-OF-DATE ***

You are missing one or more Perl modules, require newer versions, or some modules failed to load. Use CPAN to install it as described in this tutorial
```

查看必须的模块是否缺少，比如下面缺少Config::General, Font::TTF::Font, GD, GD::Polyline等
```
circos-0.67-7/bin$ ./circos -modules
ok       1.29 Carp
ok       0.36 Clone
missing            Config::General
ok       3.40 Cwd
ok      2.145 Data::Dumper
ok       2.52 Digest::MD5
ok       2.84 File::Basename
ok       3.40 File::Spec::Functions
ok       0.23 File::Temp
ok       1.51 FindBin
missing            Font::TTF::Font
missing            GD
missing            GD::Polyline
ok       2.39 Getopt::Long
ok       1.16 IO::File
ok       0.33 List::MoreUtils
ok       1.38 List::Util
missing            Math::Bezier
ok      1.998 Math::BigFloat
ok       0.06 Math::Round
missing            Math::VecStat
ok       1.03 Memoize
ok       1.32 POSIX
ok       1.08 Params::Validate
ok       1.61 Pod::Usage
missing            Readonly
ok 2013031301 Regexp::Common
missing            SVG
missing            Set::IntSpan
missing            Statistics::Basic
ok       2.41 Storable
ok       1.17 Sys::Hostname
ok       2.02 Text::Balanced
missing            Text::Format
ok     1.9725 Time::HiRes
```

检查perl的版本，如果早于5.8应该更新perl
```
circos-0.67-7/bin$ perl -v

This is perl 5, version 18, subversion 2 (v5.18.2) built for darwin-thread-multi-2level
(with 2 registered patches, see perl -V for more detail)
```

用cpan安装modules，运行cpan，第一次运行选择自动配置yes，和local::lib等待运行结束，输出信息过长，不全部显示了，另外镜像选择的时候选择yes
```
circos-0.67-7/bin$ sudo cpan
Sorry, we have to rerun the configuration dialog for CPAN.pm due to
some missing parameters. Configuration will be written to


CPAN.pm requires configuration, but most of it can be done automatically.
If you answer 'no' below, you will enter an interactive dialog for each
configuration option instead.

Would you like to configure as much as possible automatically? [yes] yes

Use of uninitialized value $what in concatenation (.) or string at /System/Library/Perl/5.18/App/Cpan.pm line 553,  line 1.

Warning: You do not have write permission for Perl library directories.

To install modules, you need to configure a local Perl library directory or
escalate your privileges.  CPAN can help you by bootstrapping the local::lib
module or by configuring itself to use 'sudo' (if available).  You may also
resolve this problem manually if you need to customize your setup.

What approach do you want?  (Choose 'local::lib', 'sudo' or 'manual')
[local::lib] local::lib

Autoconfigured everything but 'urllist'.
```

安装相应的module，GD是最难安装的，放在最后。安装的输出信息不再显示
```
cpan[1]> install Config::General
TLINDEN/Config-General-2.56.tar.gz
/usr/bin/make install  -- OK
cpan[2]> install Font::TTF::Font
MHOSKEN/Font-TTF-1.05.tar.gz
/usr/bin/make -- OK
cpan[3]> install Math::Bezier
ABW/Math-Bezier-0.01.tar.gz
/usr/bin/make install  -- OK
cpan[4]> install Math::VecStat
ASPINELLI/Math-VecStat-0.08.tar.gz
/usr/bin/make install  -- OK
cpan[5]> install Readonly
SANKO/Readonly-2.00.tar.gz
./Build install  -- OK
cpan[6]> install SVG
SZABGAB/SVG-2.63.tar.gz
/usr/bin/make install  -- OK
cpan[7]> install Set::IntSpan
SWMCD/Set-IntSpan-1.19.tar.gz
/usr/bin/make install  -- OK
cpan[8]> install Statistics::Basic
JETTERO/Statistics-Basic-1.6611.tar.gz
/usr/bin/make install  -- OK
cpan[9]> install Text::Format
SHLOMIF/Text-Format-0.59.tar.gz
./Build install  -- OK
```


*****************************星号中间的内容可以作为Mac安装GD的参考。

本来这个地方的内容有很多，但是我没搞定，让我删除了。囧，果然如官网所说，GD不好安装。
Circos官网并没有指出所有的依赖的包，比如没有告诉我还要依赖zlib什么的，导致我安装无法成功。

不过我搜到，有人把需要的模块打包在一起，直接运行install脚本就可以了。

[/wp/f4w/2020//FileAttach/2015-05-08-install-gd.tar.gz](https://raw.githubusercontent.com/ProfessionalFarmer/f4w/master/2020//FileAttach/2015-05-08-install-gd.tar.gz)

参见[http://wangqinhu.com/install-gd-on-mavericks/](http://wangqinhu.com/install-gd-on-mavericks/)

或者参见[http://www.jb51.net/os/RedHat/1286.html](http://www.jb51.net/os/RedHat/1286.html "http://www.jb51.net/os/RedHat/1286.html")

**************************
看了看circos官网的"快速开始"部分，学习了一下，顺便上自己做的一张简单的图，颜色没有调试，用的circos默认给染色体的颜色。
国内介绍circos用法的资料很少，有种要翻译circos的用法的冲动呀。可能对我而言，教程相对简单点，对纯生物的人来说，看起来可能吃力点。

![](/wp/f4w/2020/2015-05-11-circos.png) 

本文主要参考：

circos官网http://circos.ca/tutorials

http://zientzilaria.herokuapp.com/blog/2012/06/03/installing-circos-on-os-x/

http://wangqinhu.com/install-gd-on-mavericks/

http://www.jb51.net/os/RedHat/1286.html