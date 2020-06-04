---
title: Ubuntu解决0% [Waiting for headers]
date: 2020-04-16 17:09:36
tags: 
	- Linux 
categories: 
    - [操作系统,Linux,配置]
---

转载自: https://www.jianshu.com/p/122bc204f6cc

## 1.问题描述

> 更换Ubuntu的软件源 编辑/etc/apt/sources.list文件
> 执行**apt-get update**命令出现0% [Waiting for headers]问题

## 2.解决方案

```bash
sudo apt-get clean
```

