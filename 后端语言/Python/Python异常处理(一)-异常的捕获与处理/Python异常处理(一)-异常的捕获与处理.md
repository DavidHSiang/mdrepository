---
title: Python异常处理(一)-异常的捕获与处理
date: 2020-04-30 18:02:36
reward: true
declare: true
tags: 
	- Python
categories: 
	- [后端语言,Python]
---

## 异常的捕获与处理

在Python中, 使用``try``来捕获``try``中代码块的异常, 使用``except``来处理异常, 当``try``中代码块没有异常时,执行``else``代码块, 在异常的捕获处理的最后,执行``finally``代码块, 其中``else``和``finally``代码块可以省略

```python
try:
    <语句块1>
except:
    <语句块2>  # 当<语句块1>有异常时执行
else:  # 不需要时可省略
    <语句块3>  # 当<语句块1>无异常时执行
finally:  # 不需要时可省略
    <语句块4>  # 当<语句块1>和 <语句块2> 或 <语句块3> 都执行完时执行
```

