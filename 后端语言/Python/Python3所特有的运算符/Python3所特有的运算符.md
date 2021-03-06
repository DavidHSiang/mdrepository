---
title: Python3所特有的运算符
date: 2020-04-22 18:10:36
reward: true
declare: true
tags: 
	- Python
categories: 
	- [后端语言,Python]
---



## 前言

本文只描述Python3有别于其他编程语言的运算符,那些加减乘除这些"放之四海而皆准"的就不再赘述了

## 一、``//``和``**``运算符

### (1)``//``运算符

在Python中,不使用``//``表示行注释,而是使用``#``表示行注释. ``//``**在Python中是一个整除运算符.**

通常来说``整数/整数``若不能整除, 会返回商的整数部分, 返回类型是整数。

而在Python中``整数/整数``若不能整除, 会直接返回商的值, 返回类型是浮点数。若要实现只返回一个商的整数部分, 就需要使用``//``

```python
a = 1 / 2  # a的值为0.5 , 返回商
a = 1 // 2  # a的值为0 , 只返回一个商的整数部分
a //= 2  # 等价于 a = a // 2 , a 的值为 0
```

### (2)``**``运算符

``**``运算符为**幂运算符**, ``a ** b``的值为``a ^ b``

```python
x = 2 ** 3  # x 的值为8 (2的三次方)
x **= 2 # 等价于 a = a ** 2 , a 的值为 8^3 = 512
```

<!--more-->

## 二、逻辑运算符

### (1)and 与

### (2)or 或

### (3)not 非

## 三、位运算符

| 运算符          | 说明     |
| --------------- | -------- |
| ``<<``          | 按位左移 |
| ``>>``          | 按位右移 |
| ``&``           | 按位与   |
| <code>\|</code> | 按位或   |
| ``^``           | 按位异或 |
| ``~``           | 按位取反 |

## 三、字符串操作符

|  操作符及使用  |              描述              |
| :------------: | :----------------------------: |
|     x + y      |         拼接字符串x和y         |
| x * n 或 n * x |         复制n次字符串x         |
|     x in s     | 判断字符串x是否为字符串s的子串 |

