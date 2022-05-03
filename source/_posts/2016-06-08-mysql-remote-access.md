---
title: 修改MySQL远程访问权限
tags:
  - MySQL
url: archives/760/index.html
id: 760
categories:
  - Default Category
date: 2016-06-08 14:35:08
---

修改MySQL远程访问权限
=============

```mysql
grant all privileges on *.* to 'root'@'%' identified by '123456';
```

\# *.* 表示允许所有表 'root' 表示允许root用户 '%' 表示任意ip '123456' 表示密码

```
flush privileges;
```

# 刷新