---
title: NanoPi NEO2 学习笔记 1：安装、登陆、配置源
date: 2020-04-16 17:14:36
tags: 
	- NanoPi
categories: 
    - [嵌入式,NanoPi NEO2]
---

部分内容转载自:[NanoPi NEO2 学习笔记 1：安装系统、首次开机和一些设置](https://www.cnblogs.com/netube/p/10159729.html)

---

## 一、安装系统

下载官方的资料包: http://download.friendlyarm.com/nanopineo2

本文采用Ubuntu的``dd``指令烧录TF卡，若为Windows系统，可使用官方资料包中的Win32DiskImager.exe　程序进行烧录

```sh
#查看磁盘挂载
df -h
#查看dd指令的使用方法
dd --help
#卸载TF卡
umount /dev/sdc1
#查看磁盘挂载,检验是否卸载成功
df -h
#将镜像文件解压
unzip nanopi-neo2_sd_friendlycore-xenial_4.14_arm64_20191219.img.zip
#将镜像文件烧录至TF卡
sudo dd bs=4M if=nanopi-neo2_sd_friendlycore-xenial_4.14_arm64_20191219.img of=/dev/sdc
```

<!--more-->

## 二、登陆系统

登陆路由器,查看NanoPi的IP地址

```bash
ssh root@192.168.x.xxx
```

默认账号:``root``密码:``fa``

## 三、修改配置源

**注意！！！这里的源必需是ARM64的源，添加amd64的源服务器是没用的！！！很多软件都无法安装的！！！**

**arm ubuntu开发板的apt的库和普通ubuntu的库是不一样的，arm的是ubuntu-ports库**

(1)备份配置源

```bash
 sudo cp /etc/apt/sources.list /etc/apt/sources.list.old
```

(2)更换新的配置源

编辑配置文件

```bash
sudo vim /etc/apt/sources.list
```

删除原配置,添加新配置:

```bash
deb http://mirrors.ustc.edu.cn/ubuntu-ports/ xenial main multiverse restricted universe 
deb http://mirrors.ustc.edu.cn/ubuntu-ports/ xenial-backports main multiverse restricted universe 
deb http://mirrors.ustc.edu.cn/ubuntu-ports/ xenial-proposed main multiverse restricted universe 
deb http://mirrors.ustc.edu.cn/ubuntu-ports/ xenial-security main multiverse restricted universe 
deb http://mirrors.ustc.edu.cn/ubuntu-ports/ xenial-updates main multiverse restricted universe 
deb-src http://mirrors.ustc.edu.cn/ubuntu-ports/ xenial main multiverse restricted universe 
deb-src http://mirrors.ustc.edu.cn/ubuntu-ports/ xenial-backports main multiverse restricted universe 
deb-src http://mirrors.ustc.edu.cn/ubuntu-ports/ xenial-proposed main multiverse restricted universe 
deb-src http://mirrors.ustc.edu.cn/ubuntu-ports/ xenial-security main multiverse restricted universe 
deb-src http://mirrors.ustc.edu.cn/ubuntu-ports/ xenial-updates main multiverse restricted universe
```

