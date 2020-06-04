---
title: Ubuntu安装GTK+-3.0
date: 2020-04-11 14:46:36
reward: true
declare: true
tags: 
	- C/C++ 
categories: 
    - [后端语言,C/C++,GTK+]
---

## 一、安装

```bash
# 安装gcc/g++/gdb/make等基本编程工具
sudo apt-get install build-essential
# 安装GTK+3.0
sudo apt-get install libgtk-3-dev
# 安装pkg-config
sudo apt-get install pkg-config
# 安装帮助文件，方便查看帮助
sudo apt-get install devhelp
```

<!--more-->

---

## 二、检查

```bash
# 查看 pkg-config 版本
pkg-config --version
# 查看 GTK+ 版本
pkg-config --modversion gtk+-3.0
```

---

## 三、文件位置

* GTK+头文件位置：/usr/include/gtk-3.0
* 库文件位置： /usr/lib/X86_64-linux-gnu

---

## 参考文档

[怎样在Ubuntu16.04上安装GTK+-3.0](https://blog.csdn.net/singleyellow/article/details/74628428)