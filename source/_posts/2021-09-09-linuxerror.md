---
title: C++14 standard requested but CXX14 is not defined
tags:
  - Linux
url: archives/1283.html
id: 1283
categories:
  - Default Category
date: 2021-09-09 08:04:20
---


在安装R包的时候遇到报错，C++14 standard requested but CXX14 is not defined

查了很多办法，刚开始是根据https://github.com/stan-dev/rstan/issues/892修改.R下面的Makevars，

但是包另外一个错g++: error: unrecognized command line option ‘-std=c++14’

于是继续查到c++1y这个问题，但依然没有解决问题。

复盘了一下，感觉是gcc的问题，所以升级了最新的gcc

```
# 系统是CentOS
sudo yum install centos-release-scl
sudo yum install devtoolset-10
scl enable devtoolset-10 bash
```

但是装包的时候新版的gcc依然不能别识别，所以修改Makevars，最终用了如下的配置,重点是指定了新版的g++和c++的路径，这样问题就解决了
```
MAKEFLAGS = -j18

## C++ flags
CXX=g++
CXX11=g++
CXX14=/opt/rh/devtoolset-9/root/usr/bin/g++
CXX17=g++

CXXFLAGS=-O3 -march=native -Wno-ignored-attributes
CXX11FLAGS=-O3 -march=native -Wno-ignored-attributes
CXX14FLAGS=-O3 -march=native -Wno-ignored-attributes
CXX17FLAGS=-O3 -march=native -Wno-ignored-attributes

CXXPICFLAGS=-fPIC
CXX11PICFLAGS=-fPIC
CXX14PICFLAGS=-fPIC
CXX17PICFLAGS=-fPIC

CXX11STD=-std=c++11
CXX14STD=-std=c++14
CXX17STD=-std=c++17

## C flags
CC=/opt/rh/devtoolset-10/root/usr/bin/gcc
FLAGS=-O3 -march=native

## Fortran flags
FC=gfortran
F77=gfortran
FFLAGS=-O3 -march=native
FCFLAGS=-O3 -march=native
```

总结：
1，upgrade gcc

2, specify the absolute gcc and g++ path 

如果可以的话，建议把整个系统的gcc都替换成新版的

#####################################################################
\#版权所有 转载请告知 版权归作者所有 如有侵权 一经发现 必将追究其法律责任
\#Author: Jason
#####################################################################


