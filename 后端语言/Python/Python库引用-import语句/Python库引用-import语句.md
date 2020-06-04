---
title: Python库引用-import语句
date: 2020-04-28 15:55:36
reward: true
declare: true
tags: 
	- Python
categories: 
	- [后端语言,Python]
---

>  简介

库引用是Python扩充程序功能的方式, Python使用``import``关键字来实现库引用

Python库引用的方式总共有三种:

* ``import <库名>``
* ``from <库名> import <函数名>``
* ``import <库名> as <库别名>``

<!--more-->

>  库引用方式(一): ``import <库名>``

```python
# 引用库
import <库名>
# 调用库中的函数
<库名>.<函数名>(<函数参数>)
```

> 库引用方式(二): ``from <库名> import <函数名>``

```python
# 引用库
from <库名> import <函数名>
# 或
from <库名> import *  # 表示引用库中的所有函数
# 调用库中的函数
<函数名>(<函数参数>)
```

**注意:** 虽然这种方式调用库中的函数方便, 但是**容易造成函数重名的问题**

>  库引用方式(三): ``import <库名> as <库别名>``

```python
# 引用库
import <库名> as <库别名>
# 调用库中的函数
<库别名>.<函数名>(<函数参数>)
```

