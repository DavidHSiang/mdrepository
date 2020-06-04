---
title: Java10新特性var关键字
date: 2020-05-08 21:43:36
reward: true
declare: true
tags: 
	- Java
categories: 
	- [后端语言,Java]
---

从Java 10 开始, 对于局部变量, 如果可以从变量的初始值推断出他的类型, 就不再需要声明类型,只需要使用关键字var而无需指定类型

例如:

```java
String s = "123";
```

可以使用如下声明来代替:

```java
var s = "123";
```

在使用var关键字时,有几个需要注意的点:

1.建议不要对数值类型使用var,例如int、long或double, 这样可以不用担心0、0L、0.0之间的区别

2.var关键字只能用于方法中的局部变量。参数和字段的类型必须声明

