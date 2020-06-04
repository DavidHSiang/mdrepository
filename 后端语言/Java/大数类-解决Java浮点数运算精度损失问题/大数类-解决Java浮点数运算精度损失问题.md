---
title: 大数类-解决Java浮点数运算精度损失问题
date: 2020-05-08 17:07:36
reward: true
declare: true
tags: 
	- Java
categories: 
	- [后端语言,Java]
---

## 一、Java浮点数运算损失精度问题描述

在Java中, 浮点数的运算存在着误差. 例如: 0.1 + 0.2 的结果并非0.3 ,而是0.30000000000000004

```java
jshell> 0.1 + 0.2
$1 ==> 0.30000000000000004
```

这是因为, 在计算机内部, 浮点数是由二进制表示的, 而在二进制中无法精确的表示1/10 (这就好像在十进制中无法精确的表示1/3一样)

若要解决这个问题, 有两种方式,一是**四舍五入**, 二是使用**大数类**

使用四舍五入有可能会带来误差,若在数值计算中, 不允许有任何舍入误差,就应该使用**大数类**

<!--more-->

## 二、大数类

### (1)简介

如果基本的整数和浮点数的精度不能够满足需求, 那边可以使用java.math包中的两个类:``BigInteger``和``BigDecimal``

``BigInteger``实现任意精度的整数运算

``BigDecimal``实现任意精度的浮点数运算

### (2)构造

使用静态的.valueOf方法可以将普通的数值转换为大数

```java
BigDecimal x = BigDecimal.valueOf(0.1);
BigInteger a = BigInteger.valueOf(100);
```

对于更大的数,可以使用一个带字符串的构造器:

```java
BigDecimal x = BigDecimal.valueOf("0.656546545646541");
BigInteger a = BigInteger.valueOf("1006546456464654654645645");
```

### (3)大数类运算

> ``BigInteger``运算相关方法:

* 加: ``BigInteger add(BigInteger other)``

* 减: ``BigInteger subtract(BigInteger other)``

* 乘: ``BigInteger multiply(BigInteger other)``

* 除:``BigInteger divide(BigInteger other)``

* 取余: ``BigInteger mod(BigInteger other)``

> ``BigDecimal``运算相关方法:

* 加: ``BigDecimal add(BigDecimal other)``

* 减: ``BigDecimal subtract(BigDecimal other)``

* 乘: ``BigDecimal multiply(BigDecimal other)``

* 除:``BigDecimal divide(BigDecimal other)`` 若商是无限循环小数, 会抛异常

* 除:``BigDecimal divide(BigDecimal other, RoundingMode mode)``若商是无限循环小数, 会根据``RoundingMode mode``进行舍入, 若mode参数为``RoundingMode.HALF_UP``表示舍入方法为四舍五入

### (4)解决Java浮点数运算精度损失问题示例

```java
jshell> 0.1 + 0.2
$1 ==> 0.30000000000000004

jshell> BigDecimal x = BigDecimal.valueOf(0.1)
x ==> 0.1
jshell> BigDecimal y = BigDecimal.valueOf(0.2)
y ==> 0.2
jshell> BigDecimal z = x.add(y) 
z ==> 0.3
```

## 参考文档

[Java核心技术~卷一-第三章3.9大数](#)

