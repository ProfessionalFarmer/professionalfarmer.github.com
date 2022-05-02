---
title: Matlab error when running GISTIC
tags:
  - CNV
  - Matlab
url: archives/1092.html
id: 1092
categories:
  - Default Category
date: 2020-03-27 13:50:36
---

If you instal MCR (MATLAB Compiler Runtime) provided by GISTIC package, may have the following error. This error could disrupt GISTIC.
**libGL error: failed to load driver: swrast**

If this situation occurs, rename the file found at **" _$MATLAB_ROOT_/sys/os/glnxa64/libstdc++.so.6" to "libstdc++.so.6.old"**, This forces MATLAB to use the OS library.

Works for me.

Ref:
[https://ww2.mathworks.cn/matlabcentral/answers/296999-libgl-error-unable-to-load-driver-in-ubuntu-16-04-while-running-matlab-r2013b](https://ww2.mathworks.cn/matlabcentral/answers/296999-libgl-error-unable-to-load-driver-in-ubuntu-16-04-while-running-matlab-r2013b)

[GISTIC2.0 facilitates sensitive and confident localization of the targets of focal somatic copy-number alteration in human cancers](http://portals.broadinstitute.org/cgi-bin/cancer/publications/pub_paper.cgi?mode=view&paper_id=216&p=t)