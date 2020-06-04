---
title: Python函数(三)-变量作用域和匿名函数
date: 2020-04-30 19:19:36
reward: true
declare: true
tags: 
	- Python
categories: 
	- [后端语言,Python]
---

## 一、全局变量和局部变量

### (1)局部变量

局部变量, 是函数内定义的变量, 只在定义他的函数内生效, 如:

```python
def f(m, n = 0):
    x = 1
    return m + n + x
f(1, 2)
```

在上述代码中, 函数f中的x就是一个局部变量

**在函数内,不能直接修改全局变量, 若直接给全局变量赋值, 会被当做创建一个局部变量, 他的名称与全局变量相同, 并不会修改全局变量。**当局部变量与全局变量名称相同时, 在函数内部使用局部变量, 如:

```python
x = 3
def f(m, n = 0):
    x = 1  # 定义一个局部变量, 而非修改全局变量
    return m + n + x
print(f(1, 2))  # 输出结果为4
print(x)  # 输出结果为3
```

<!--more-->

### (2)全局变量

全局变量是函数外定义的变量, 在程序的任何位置都可以被访问。在函数内部只能访问全局变量, 不能修改全局变量, 若要修改全局变量, 需使用关键字``global``

```python
x = 3
def f(m, n = 0):
    global x
    x = 1  # 定义一个局部变量, 而非修改全局变量
    return m + n + x
print(f(1, 2))  # 输出结果为4
print(x)  # 输出结果为1
```

## 二、匿名函数

Python中匿名函数使用lambda语句来定义, lambda语句的格式为:

```python
<函数名> = lambda <参数>: <表达式>
```

上述语句等价于:

```python
def <函数名>(<参数>):
    return <表达式>
```

> 匿名函数实例

```python
>>> f = lambda x, y : x + y
>>> f(10, 15)
25
>>> f = lambda : "lambda函数"
>>> print(f())
lambda函数
```

