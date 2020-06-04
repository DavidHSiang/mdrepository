---
title: Python海龟绘图-turtle库学习笔记(二)-画笔控制函数
date: 2020-04-28 16:33:36
reward: true
declare: true
tags: 
	- Python
categories: 
	- [后端语言,Python]
---

## 抬起画笔

```python
turtle.penup()  # 抬起画笔(海龟在飞行)
turtle.pu()  # 别名
```

## 落下画笔

```python
turtle.pendown()  # 落下画笔(海龟在爬行)
turtle.pd()  # 别名
```

<!--more-->

## 改变画笔宽度

```python
turtle.pensize(width)  # 改变画笔宽度(改变海龟的腰围)
turtle.width(width)  # 别名
```

## 改变画笔颜色

```python
# color为颜色字符串或RGB值
# 改变画笔颜色(为海龟涂装)
turtle.pencolor(color)
```

color参数的三种形式:

* 颜色字符串: ``turtle.pencolor("purple")``
* RGB的小数值: ``turtle.pencolor(0.5, 0.5, 0.5)``
* RGB的元组值: ``turtle.pencolor((0.5, 0.5, 0.5))``