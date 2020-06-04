---
title: Java开发环境不再需要配置classpath
date: 2020-5-2 23:27:36
tags: 
	- Java
categories: 
	- [后端语言,Java]
---

本文转载自: [Java开发环境不再需要配置classpath！](https://www.cnblogs.com/ideal-20/p/11050114.html)https://www.cnblogs.com/ideal-20/p/11050114.html

## 前言：

之前发布了关于java开发环境配置的文章，经过与网友的交流，我了解到在jdk1.5以后，java开发环境配置的时候，确实不需要对classpath进行配置，但市面上的书籍，以及一些博客、还是老一套，继续推荐配置classpath，并且关于不需要配置classpath网络上没有什么完整细致，能令人信服的答案，所以我查阅了一些资料以及与别人交流，今天和大家分享一下这些内容。

<!--more-->

### 原配置代码：

> .;%Java_Home%\bin;%Java_Home%\lib\dt.jar;%Java_Home%\lib\tools.jar

#### 原代码详解：

Java_Home代表了我们jdk的路径

- dt.jar是关于运行环境的类库，主要是用于swing的包，如果不使用可以不配置。
- tools.jar是工具类库,它在编译和运行一个类时被使用

当我们配置classpath后，系统会根据我们所配置的classpath加载类

例如：在我们使用javac命令编译程序时，系统加载tools.jar其实就封装了下面这样一条命令

> javac XXX.java

> java -Classpath=%JAVA_HOME%\lib\tools.jar  xx.xxx.Main  XXX.java

当然tools的功能可不止这一点，但是确实它为我们提供了很多便利

### 我们不再需要配置classpath了！

在JDK1.5以后，classpath并不是必须配置了，在JDK1.5之前，是没有办法在当前目录下加载类的（找不到  JDK目录下lib文件夹中的.jar文件），所以我们需要通过配置classpath，但JDK1.5之后，JRE能自动搜索目录下类文件，并且加载dt.jar和tool.jar的类。

### 官方文档解释（JDK Tools and Utilities）

> The class path tells the JDK tools and applications where to find  third-party and user-defined classes that are not extensions or part of  the Java platform. See The Extension Mechanism at

> 类路径告诉JDK工具和应用程序在哪里可以找到第三方和用户定义的类，这些类既不是Java平台的扩展，也不是Java平台的一部分。参见扩展机制

> If you upgrade from an earlier release of the JDK, then your startup  settings might include CLASSPATH settings that are no longer needed. You should remove any settings that are not application-specific, such as  classes.zip. Some third-party applications that use the Java Virtual  Machine (JVM) can modify your CLASSPATH environment variable to include  the libraries they use. Such settings can remain.

> 如果您从JDK的早期版本升级，那么您的启动设置可能包括不再需要的类路径设置。您应该删除任何与应用程序无关的设置，比如classes.zip。一些使用Java虚拟机(JVM)的第三方应用程序可以修改类路径环境变量，以包含它们使用的库。这样的设置可以保留。

> You can change the class path by using the -classpath or -cp option  of some Java commands when you call the JVM or other JDK tools or by  using the CLASSPATH environment variable. See JDK Commands Class Path  Options. Using the -classpath option is preferred over setting the  CLASSPATH environment variable because you can set it individually for  each application without affecting other applications and without other  applications modifying its value. See CLASSPATH Environment Variable.

> 在调用JVM或其他JDK工具时，可以使用一些Java命令的-classpath或-cp选项，或者使用CLASSPATH环境变量，来更改类路径。参见JDK命令类路径选项。使用-classpath选项优于设置CLASSPATH环境变量，因为您可以为每个应用程序单独设置它，而不影响其他应用程序，也不需要其他应用程序修改它的值。参见CLASSPATH环境变量。

通过官方的文档说明我们可以看到，rt.jar和tool.jar这两种属于java平台自身的包就不需要添加到classpath中，只有一些第三方类或者自定义类需要，也并不推荐使用配置CLASSPATH的方法，更推荐使用-classpath选项

## 总结：

**在JDK1.5之后的版本，配置Java环境变量的时候我们不再需要配置classpath，只需要配置Java_Home以及path即可！**