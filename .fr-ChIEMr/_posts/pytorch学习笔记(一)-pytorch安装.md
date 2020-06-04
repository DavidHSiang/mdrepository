---
title: pytorch学习笔记(一)-pytorch安装
date: 2020-04-19 12:50:36
reward: true
declare: true
tags: 
	- Pytorch
categories: 
  - [人工智能,Pytorch]
---

## 一、Pytorch官网

Pytorch官网:https://pytorch.org/

官网下载页: https://pytorch.org/get-started/locally/

## 二、使用conda安装

### (0)新建conda环境

```bash
# 新建conda环境
conda create -n pytorch python=3
# 转换到pytorch环境
conda activate pytorch
```

<!--more-->

### (1)官方安装

选择安装的方式

![pytorch安装](img/pytorch安装.png)

复制官方的安装命令:

```bash
conda install pytorch torchvision cpuonly -c pytorch
```

### (2)使用清华镜像安装

在国内使用官方的安装命令安装会很慢,这里可以使用清华conda镜像

#### 1.添加清华镜像

```bash
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/pytorch/
conda config --add channels https://mirrors.sjtug.sjtu.edu.cn/anaconda/pkgs/main/
conda config --add channels https://mirrors.sjtug.sjtu.edu.cn/anaconda/pkgs/fr
```

#### 2.安装Pytorch

复制命令并将命令删去 -c pytorch 即可自动从清华源下载安装包：

```bash
conda install pytorch torchvision cpuonly
```