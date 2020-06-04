---
title: Python布尔类型
date: 2020-04-22 14:54:36
reward: true
declare: true
tags: 
	- Python
categories: 
	- [后端语言,Python]
---

## bool类型介绍

Python中的bool类型**只有两个取值**:``True``和``false``。实际上bool类型是一种**特殊的整型**,``True``对应``1``,``False``对应``0``

## bool类型转换

Python的任何对象都可以转换为bool类型, 若要进行转换,符合一下条件的数据都会被转换为``False``

(1)None

(2)任何为0的数字类型, 如``0``、``0.0``、``0j``

(3)任何空序列, 如``""``、``[]``、``()``

(4)任何空字典, 如``{}``

(5)用户定义的类实例, 如类中定义了``__bool__()``或``__len__()``

**除以上对象外,其他的对象都会被转换为**``True``

可以使用``bool()``来检查对象的bool值:

```python
>>> bool(None)
False
>>> bool(0)
False
>>> bool(1)
True
```

