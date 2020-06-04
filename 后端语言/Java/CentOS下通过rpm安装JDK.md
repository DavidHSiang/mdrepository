---
title: CentOS下通过rpm安装JDK
copyright: true
date: 2020-04-10 22:29:36
reward: true
declare: true
tags: 
	- Java
categories: 
    - [后端语言,Java]
---

## 一、下载

官网下载地址：https://www.oracle.com/java/technologies/javase-downloads.html

华为云镜像下载地址：https://repo.huaweicloud.com/java/jdk/

<!--more-->

## 二、清理系统默认自带的 jdk

```bash
# 查看自带的 jdk
rpm -qa | grep jdk
# 卸载 jdk
yum remove XXX
```

## 三、赋予权限

```bash
# 赋予 rpm 安装包权限
chmod 777 jdk-7u80-linux-x64.rpm
```

## 四、安装

```bash
# 使用rpm命令安装
rpm -ivh jdk-7u80-linux-x64.rpm
```

## 五、配置环境变量

```bash
# 打开环境变量配置文件
vi /etc/profile
```

配置环境变量：JAVA_HOME、CLASSPATH、PATH，在profile末尾添加配置

```bash
# JAVA_HOME值为jdk安装路径
export JAVA_HOME=/usr/java/jdk1.7.0_80
export CLASSPATH=.:$JAVA_HOME/jre/lib/rt.jar:$JAVA_HOME/jre/lib/dt.jar:$JAVA_HOME/jre/lib/tools.jar
# PATH变量下添加 jdk 目录下的 bin 目录
export PATH=$JAVA_HOME/bin:$PATH
```

使环境变量生效

```bash
source /etc/profile
```

## 六、验证

```bash
# 验证安装是否成功
java -version
```