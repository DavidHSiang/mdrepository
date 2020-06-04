---
title: Python复数类型
date: 2020-04-22 14:12:36
reward: true
declare: true
tags: 
	- Python
categories: 
	- [后端语言,Python]
---

## 一、数学中的负数

**复数**，为[实数](https://zh.wikipedia.org/wiki/實數)的延伸，它使任一[多项式](https://zh.wikipedia.org/wiki/多項式)[方程](https://zh.wikipedia.org/wiki/方程)都有[根](https://zh.wikipedia.org/wiki/根_(数学))。复数当中有个“[虚数单位](https://zh.wikipedia.org/wiki/虛數單位) ``i``，它是``-1``的一个[平方根](https://zh.wikipedia.org/wiki/平方根)，即``i ^ 2 = -1``。任一复数都可表达为``x + yi``，其中``x``及``y``皆为实数，分别称为复数之“实部”和“虚部”。

复数的发现源于[三次方程](https://zh.wikipedia.org/wiki/三次方程)的根的表达式。数学上，“复”字表明所讨论的[数域](https://zh.wikipedia.org/wiki/數體)为复数，如[复矩阵](https://zh.wikipedia.org/wiki/矩陣)、[复变函数](https://zh.wikipedia.org/wiki/复变函数)等。

> 定义

复数通常写为如下形式：

```
a + bi
```

这里的``a``和``b``是[实数](https://zh.wikipedia.org/wiki/实数)，而``i``是[虚数单位](https://zh.wikipedia.org/wiki/虛數單位)，它有着性质``i ^ 2 = -1``。实数``a``叫做复数的**实部**，而实数``b``叫做复数的**虚部**。实数可以被认为是虚部为零的复数；就是说实数``a``等价于复数``a +0i``。实部为零且虚部不为零的复数也被称作“纯虚数”；而实部不为零且虚部也不为零的复数也被称作“非纯虚数”或“杂虚数”。

-- 节选自[维基百科](https://zh.wikipedia.org/wiki/%E5%A4%8D%E6%95%B0_(%E6%95%B0%E5%AD%A6))

<!--more-->

## 二、Python复数类型

在Python中,存在着复数数字类型, 它的一般形式为: 

```python
real + imagj
```

``real``表示实部, ``imag``表示虚部. ``j``或``J``表示虚数单位. 虚部后必须有后缀``j``或``J``

> 复数的创建

1.直接创建

```python
num = 3 + 2j  # 3为实部, 2为虚部
```

2.通过内置函数``complex()``创建

```python
num = complex(3, 2)  # 3为实部, 2为虚部
```

复数类型可以通过``<复数类型>.real``和``<复数类型>.imag``来获得复数的实部和虚部:

```python
>>> z = 1 + 2j
>>> z.real
1.0
>>> z.imag
2.0
```

## 参考文档

[维基百科-复数](https://zh.wikipedia.org/wiki/%E5%A4%8D%E6%95%B0_(%E6%95%B0%E5%AD%A6)):https://zh.wikipedia.org/wiki/%E5%A4%8D%E6%95%B0_(%E6%95%B0%E5%AD%A6)

