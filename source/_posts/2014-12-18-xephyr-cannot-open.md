---
title: Xephyr cannot open host display. Is DISPLAY set?
tags:
  - Xephyr
url: archives/700/index.html
id: 700
categories:
  - Default Category
date: 2014-12-18 19:18:39
---

After Mac update to OS X Yosemite Version 10.10, I can't run Xephyr. 

Error occurs 

Xephyr cannot open host display. Is DISPLAY set 

I have tried to fix it by "export DISPLAY=:1", or something else. However, no approach to fix it. I tried to update X11 before giving up. 

Ah, it worked! 

I remember downgrading X11 also solved another problem several monthes ago. So update or degrade your X11 might be a way to solve your problem.