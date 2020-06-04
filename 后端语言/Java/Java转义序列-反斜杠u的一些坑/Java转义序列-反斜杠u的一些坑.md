---
title: Java转义序列\u的一些坑
date: 2020-05-08 18:28:36
reward: true
declare: true
tags: 
	- Java
categories: 
	- [后端语言,Java]
---

在java的转义序列中, ``\u``是一个十分特殊的存在, ``\u``与其他的转义字符有两点不同:

> 1.\u可以出现在引号字符常量或字符串之外

例如: main函数可以写成:

```java
public static void main(String\u005B\u005D args){
    ........
}
```

左中括号``[``的Unicode码为005B, 右中括号``]``的Unicode码为005D

>  2.\u会在解析代码之前得到处理

**\u会在解析代码之前得到处理!!!**这个十分重要, 例如:双引号"的Unicode码为0022, 字符串"\u0022 + \u0022"的内容并不是"+"而是一个空字符串, \u0022会在解析之前转换为",  ``""+""``的值是一个空串

<!--more-->

同时还要注意**注释**中的\u

例如:

```java
// \u000A is a newline
```

这会产生一个语法错误, 因为在读程序时\u000A会替换为一个换行符, ``// \u000A is a newline``等价于:

```java
// 
is a newline
```

很显然, is a newline不是java的语句,而编译器会把他当做是一条要执行的语句来看待

类似的,下面这个注释也会产生一个语法错误:

```java
// look inside c:\users
```

这是因为\u后面并没有跟着4个十六进制数

### 参考文档

[Java核心技术~卷一-P32-3.3.3-char类型](#)