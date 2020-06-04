---
title: JShell-Java9新增编程工具
date: 2020-05-08 16:40:36
reward: true
declare: true
tags: 
	- Java
categories: 
	- [后端语言,Java]
---

## JShell简介

JShell是Java 9 新增的一个交互式的编程环境工具。它这是Java提供的交互式的编程环境。可以使java想Python一样, 直接输入表达式并查看其执行结果

## 相关操作

### 启动JShell

想要使用JShell,只需在命令行键入命令``jshell``即可, 需要注意的是,要确保本机安装了JDK且版本在Java 9 及以上

```bash
~$ jshell
|  欢迎使用 JShell -- 版本 11.0.7
|  要大致了解该版本, 请键入: /help intro

jshell> 
```

<!--more-->

### 查看帮助

启动jshell后, 可以通过``/help``指令来查看帮助

```bash
jshell> /help
|  键入 Java 语言表达式, 语句或声明。
|  或者键入以下命令之一:
|  /list [<名称或 id>|-all|-start]
|  	列出您键入的源
|  /edit <名称或 id>
|  	编辑源条目
.....
```

### 执行表达式

```bash
jshell> 1 + 1
$1 ==> 2
```

在jshell中键入一个表达式,jshell会自动打印表达式计算的结果, 打印格式为:``$数字 ==> 结果``

在之后的语句中,可以使用``$数字 ``来得到之前计算的结果, 例如:

```bash
jshell> 1 + 1
$1 ==> 2

jshell> $1 + 1
$2 ==> 3
```

### 退出JShell

使用``/exit``语句退出JShell