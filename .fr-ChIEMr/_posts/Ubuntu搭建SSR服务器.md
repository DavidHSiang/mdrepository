---
title: Ubuntu搭建SSR代理服务器
date: 2020-04-08 12:10:36
reward: true
declare: true
tags: 
	- 科学上网
categories: 
    - [科学上网,SSR]
---

> 本文讲解如何在Ubuntu上搭建SSR代理服务器

### 0. 安装SSR代理软件

```
wget -N --no-check-certificate https://raw.githubusercontent.com/ToyoDAdoubi/doubi/master/ssr.sh && chmod +x ssr.sh && bash ssr.sh
```

<!--more-->

![下载SSR脚本](img/下载SSR脚本.png)

### 1. 选择安装SSR

>输入1，安装SSR

![安装SSR脚本](img/安装SSR脚本.png)

-----

### 2. 设置代理的端口号

>输入要用于代理的端口

![设置代理端口](img/输入代理端口.png)

-----

### 3. 设置代理的密码

>输入代理的密码

![设置代理的密码](img/设置代理的密码.png)

-----

### 4. 设置加密方式

>设置加密方式

![设置加密方式](img/设置加密方式.png)

-----

### 5. 设置协议

>输入代理的协议

![设置协议](img/设置协议.png)

-----

### 6. 设置协议的兼容性

>输入"y",表示兼容

![设置协议的兼容性](img/设置协议的兼容性.png)

-----

### 7. 设置混淆方式

>输入混淆的方式

![设置混淆方式](img/设置混淆方式.png)

-----

### 8. 设置同时可连接的设备数

>设置设备数

![设置设备数](img/设置可连接的设备数.png)

-----

### 9. 设置单端口的速度上限

>设置单端口的速度上限(默认是无上限)

![设置单端口的速度上限](img/设置单线程速度上限.png)

-----

### 10. 设置总速度的上限

>设置总速度的上限

![设置总速度的上限](img/设置总速度上限.png)

-----

### 代理服务器搭建完成

-----

### 参考文档

[Ubuntu16.04搭建SSR服务器+锐速](https://www.lstazl.com/ubuntu16-04%E6%90%AD%E5%BB%BAssr%E6%9C%8D%E5%8A%A1%E5%99%A8%E9%94%90%E9%80%9F/)

-----
