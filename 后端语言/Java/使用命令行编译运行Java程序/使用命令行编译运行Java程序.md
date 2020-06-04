---
title: 使用命令行编译运行Java程序
date: 2020-05-08 14:58:36
reward: true
declare: true
tags: 
	- Java
categories: 
	- [后端语言,Java]
---

## 一、检查JDK安装

查看javac(java编译器)的版本

```bash
javac --version
```

若显示找不到指令,首先查看java版本:

```bash
java --version
```

若Java版本无显示,则先检查JDK是否安装, 若JDK已经安装了,查看环境变量是否配置正确

若Java版本有显示,那么有可能是因为只安装了JRE(Java运行时环境)而没有安装JDK(Java开发环境),首先查看Java安装路径

```bash
java -verbose
[0.006s][info][class,load] opened: /usr/lib/jvm/java-11-openjdk-amd64/lib/modules
[0.006s][info][class,load] opened: /usr/share/java/java-atk-wrapper.jar
[0.026s][info][class,load] java.lang.Object source: shared objects file
[0.026s][info][class,load] java.io.Serializable source: shared objects file
[0.026s][info][class,load] java.lang.Comparable source: shared objects file
[0.026s][info][class,load] java.lang.CharSequence source: shared objects file
......
```

查看Java安装路径下的bin目录

```bash
ls /usr/lib/jvm/java-11-openjdk-amd64/bin/
```

若bin目录下没有``javac``这个文件,则说明只安装了JRE, 需要再安装JDK. 在Windows下,安装JDK可通过官网下载安装包进行安装, 在Linux下可以通过``apt``或``yum``进行安装:

```bash
sudo apt install default-jdk            jianc
sudo apt install openjdk-11-jdk-headless
sudo apt install ecj                    
sudo apt install openjdk-8-jdk-headless 
```

若bin目录下有``javac``这个文件,则要检查环境变量的配置, 如果还不行就重新安装JDK

<!--more-->

最后,再次检查Java编译器是否安装成功:

```bash
javac --version
```

## 二、编写示例文件Hello.java

编写示例文件Hello.java,实现一个最基本的打印输出功能

```bash
vim Hello.java
```

> Hello.java

```java
public class Hello
{
        public static void main(String[] args)
        {
                System.out.println("Hello World!");
        }
}
```

其中``public class Hello``的Hello是类名,需与java文件名相同, ``main``是程序入口,``System.out.println("...");``打印一条语句

## 三、编译并运行程序

使用Java编译器编译java源文件

```bash
javac Hello.java 
```

编译完成后, 会生成一个Hello.class字节码文件

通过java指令运行Hello类中的main静态方法

```bash
java Hello
```

输出:

```
Hello World!
```

**注意:**运行程序时,只需要指定类名,**不要带扩展名``.java``或``.class``**

## 四、常见错误

* 如果手工输入源程序,一定要注意正确的输入**大小写**. 例如, 类名为Hello, 而不是hello或HELLO
* 编译器需要一个文件名,而**运行时,只需要指定类名,不需要带扩展名.java或.class**
* 如果看到诸如Bad command or file name 或 javac:command not found之类的消息,就反复检查安装是否有问题,特别是环境变量的配置
* 如果javac报告了一个错误,指出无法找到Hello.java就应该检查目录中是否存在这个文件
  * Linux下使用``ls``指令查看当前目录下的文件,要注意是否有大小写的错误
  * Windows下使用``dir``查看当前目录下的文件. 若用图形界面需要注意是否有隐藏扩展名的问题
* 运行程序之后,如果遇到关于java.lang.NoClassDefFoundError的错误信息, 应该仔细检查出问题的类名
  * 如果收到关于hello(h为小写)的错误信息,应该注意区分大小写
  * 如果遇到有关Hello/java的错误信息,这说明你错误的键入了``java Hello.java``应该重新执行命令``java Hello``
* 如果键入``java Hello``而虚拟机没有找到Hello类,就应该检查是否有人设置了系统的CLASSPATH环境变量, 在java1.5以后不在需要设置CLASSPATH也不推荐设置

## 参考文档

[Java核心编程~卷一-第二章2.2使用命令行工具](#)