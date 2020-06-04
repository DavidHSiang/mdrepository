---
title: Python使用type()函数查看数据的类型
date: 2020-04-22 15:16:36
reward: true
declare: true
tags: 
	- Python
categories: 
	- [后端语言,Python]
---

在Python中, 可以使用``type()``类型来查看数据的类型:

```Python
>>> type(3)
<class 'int'>
>>> type("123")
<class 'str'>
>>> type(True)
<class 'bool'>
>>> x = 1 + 2j
>>> type(x)
<class 'complex'>
```

