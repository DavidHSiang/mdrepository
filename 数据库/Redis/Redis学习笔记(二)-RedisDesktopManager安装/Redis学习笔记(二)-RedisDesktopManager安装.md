---
title: Redis学习笔记(二)-RedisDesktopManager安装
date: 2020-05-30 10:22:36
tags: 
	- Redis
categories: 
	- [数据库,Redis]
---

转载自[Ubuntu下安装RedisDesktopManager](https://www.cnblogs.com/banbosuiyue/p/12411004.html) : https://www.cnblogs.com/banbosuiyue/p/12411004.html

### (1)RedisDesktopManager简介

RedisDesktopManager是Redis的图形化管理工具

RedisDesktopManager 官网: https://redisdesktop.com/

RedisDesktopManager 官方Github: https://github.com/uglide/RedisDesktopManager

<!--more-->

### (2)Ubuntu下安装RedisDesktopManager

​		首先,可以尝试在Ubuntu中应用商店搜RedisDesktopManager然后下载,当然, 我当时下载的时候直接卡住了, 所以就改用了手动安装

#### 1.下载安装包

​		下载redis-desktop-manager_0.8.3-120_amd64.deb安装包, 百度云地址: 

​		链接：https://pan.baidu.com/s/1KTuU2fz2DL0puT29cKrQtA  提取码：fyei 

#### 2.执行安装命令

```bash
sudo dpkg -i redis-desktop-manager_0.8.3-120_amd64.deb
```

会有以下报错,原因是依赖包没有安装:

```bash
正在选中未选择的软件包 redis-desktop-manager。
(正在读取数据库 ... 系统当前共安装有 175612 个文件和目录。)
正准备解包 redis-desktop-manager_0.8.3-120_amd64.deb  ...
正在解包 redis-desktop-manager (0.8.3-120) ...
dpkg: 依赖关系问题使得 redis-desktop-manager 的配置工作不能继续：
 redis-desktop-manager 依赖于 zlibc；然而：
  未安装软件包 zlibc。
 redis-desktop-manager 依赖于 libpng12-0；然而：
  未安装软件包 libpng12-0。
 redis-desktop-manager 依赖于 libicu52；然而：
  未安装软件包 libicu52。
 redis-desktop-manager 依赖于 libssh2-1；然而：
  未安装软件包 libssh2-1。
 
dpkg: 处理软件包 redis-desktop-manager (--install)时出错：
 依赖关系问题 - 仍未被配置
正在处理用于 gnome-menus (3.13.3-11ubuntu1.1) 的触发器 ...
正在处理用于 desktop-file-utils (0.23-1ubuntu3.18.04.2) 的触发器 ...
正在处理用于 mime-support (3.60ubuntu1) 的触发器 ...
在处理时有错误发生：
 redis-desktop-manager
```

#### 3.安装依赖包

```bash
sudo apt-get install zlibc
```

​		当我们使用命令``sudo apt-get install zlibc``安装时,会出现以下报错

```bash
正在读取软件包列表... 完成
正在分析软件包的依赖关系树       
正在读取状态信息... 完成       
您也许需要运行“apt --fix-broken install”来修正上面的错误。
下列软件包有未满足的依赖关系：
 redis-desktop-manager : 依赖: libpng12-0 但无法安装它
                         依赖: libicu52 但无法安装它
                         依赖: libssh2-1 但是它将不会被安装
E: 有未能满足的依赖关系。请尝试不指明软件包的名字来运行“apt --fix-broken install”(也可以指定一个解决办法)。
```

​		执行它所提示的语句

```bash
sudo apt --fix-broken install
```

​		安装其余的三个包

```bash
sudo apt-get install libpng12-0
sudo apt-get install libicu52
sudo apt-get install libssh2-1
```

​		如果出现以下提示, 可以去浏览器Ubuntu-软件包网站下载这些依赖包 , 网址https://packages.ubuntu.com/bionic/amd64/zlibc/download , 搜索并下载依赖包, 然后用``sudo dpkg -i 软件包名``安装依赖包

```bash
...
没有可用的软件包 libpng12-0，但是它被其它的软件包引用了。
...
```

#### 4.安装RedisDesktopManager

​	安装完这些依赖包之后,就可以安装RedisDesktopManager了

```bash
sudo dpkg -i redis-desktop-manager_0.8.3-120_amd64.deb
```

