---
title: Python流程控制
date: 2020-04-22 21:08:36
reward: true
declare: true
tags: 
	- Python
categories: 
	- [后端语言,Python]
---

## 概述

Python流程控制的语法格式与一般的编程语言不同, Python使用**缩进**来表达代码间的所属关系

## 一、if 语句

### (1)``if``语句

```python
if 条件表达式:
    代码块  # 代码块前面有1个缩进(4个空格)
```

### (2)if...else语句

```python
if 条件表达式:
    代码块  # 1个缩进
else:
    代码块  # 1个缩进
```

### (3)if...elif...else

```python
if 条件表达式:
    代码块  # 1个缩进
elif 条件表达式:
    代码块  # 1个缩进
else:
    代码块  # 1个缩进
```

### (4)if嵌套

```python
if 条件表达式:
    代码块  # 1个缩进
    if 条件表达式:  # 1个缩进
        代码块  # 2个缩进
```

### (5)... if ... else ... 紧凑形式

如果``if``和``else``要执行的语句都只有一条, 且不是赋值语句, 就可以使用... if ... else ... 的紧凑形式:

```python
# 如果条件成立, 则执行语句1, 否则执行语句2
语句1 if 条件判断 else 语句2
```

**注意:**语句1和语句2不能是赋值语句

<!--more-->

## 二、for循环

### (1)for循环语法

```python
for 临时变量 in 需要遍历的序列:
    代码块  # 1个缩进
```

> 补充知识:range()函数

### (2)for循环与range()函数结合使用

range()函数语法:

```python
range(start, stop, step)
# start默认值: 0
# step默认值: 1
# stop无默认值
```

作用: 创建一个步长为``step``,从``start``开始``stop``结束,不包括``stop``的整数列表

**for循环经常和range()函数一起使用,来指定循环的次数**

```python
for 临时变量 in range(10):  # 循环十次
    代码块  # 1个缩进
```

### (3)for循环嵌套

```python
for 临时变量 in range(10):  # 循环十次
    代码块  # 1个缩进
    for 临时变量 in range(10):  # 循环十次 , 1个缩进
        代码块  # 2个缩进
```

### (4)for...else语法

当for循环正常执行完(即 for 不是通过``break``跳出而中断的)时, 执行``else``中的代码

```python
# 当十次循环没有执行break时,执行else下的语句
for 临时变量 in range(10):  # 循环十次
    if 条件表达式:   # 1个缩进
        break # 跳出循环, 2个缩进
else:
    代码块  # 1个缩进
```

## 三、while循环

### (1)while循环语法

```python
while 条件表达式:
    代码块  # 1个缩进
```

### (2)while循环嵌套

```python
while 条件表达式:
    代码块  # 1个缩进
    while 条件表达式:  # 1个缩进
        代码块  # 2个缩进
```

### (3)while...else语法

类似于for...else

当while循环正常执行完(即 while 不是通过``break``跳出而中断的)时, 执行``else``中的代码

```python
# 当循环没有执行break时,执行else下的语句
while 条件表达式:
    代码块  # 1个缩进
    if 条件表达式:   # 1个缩进
        break # 跳出循环, 2个缩进
    代码块  # 1个缩进
else:
    代码块  # 1个缩进
```

