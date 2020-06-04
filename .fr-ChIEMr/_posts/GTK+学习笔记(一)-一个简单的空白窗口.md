---
title: GTK+学习笔记(一)-一个简单的空白窗口
date: 2020-04-11 14:55:36
reward: true
declare: true
tags: 
	- C/C++
categories: 
    - [后端语言,C/C++,GTK+]
---

## 一、创建

```bash
# 创建文件 exam-0.1.c
vim exam-0.1.c
```

## 二、编写

> exam-0.1.c

```c
#include <gtk/gtk.h>

int main ( int argc , char *argv[] ) {
    gtk_init( &argc , &argv );
    GtkWidget *window = gtk_window_new( GTK_WINDOW_TOPLEVEL );
    gtk_widget_show( window );

    gtk_main();
    return 0;
}
```

<!--more-->

## 三、编译

用gcc直接编译，默认只找标准库，而我们刚才写的代码需要依赖GTK相应的库。

因此，gcc编译时，需要加上\`pkg-config --cflags --libs gtk+-3.0\`

```bash
# 用gcc编译文件
gcc  exam-0.1.c  -o  exam-0.1  `pkg-config --cflags --libs gtk+-3.0`

# pkg-config 是一个为已经安装的包提供了include，以及实际库安装的位置编译选项的输出和管理的工具；
# --cflags 选项作用为自动获得预处理参数，如宏定义，头文件的位置；
# --libs 选项作用为自动获得链接参数，如库及依赖的其它库的位置，文件名及其它一些连接参数；
# gtk+-3.0 选项作用为指定GTK版本
```

## 四、源码解析

```c
// 引用头文件gtk/gtk.h
// gtk/gtk.h 包含 GTK+ 中所有的控件、变量、函数和结构
#include <gtk/gtk.h>

// main函数，程序入口函数
// 参数 argc : 通过命令行传递给应用程序的参数个数
// 参数 argv[] : 通过命令行传递给应用程序的参数数组
int main ( int argc , char *argv[] ) {
    
    //gtk_init( &argc , &argv )是在每个Gtk应用程序都要调用的函数
    // 检查通过命令行传递给应用程序的参数，自动完成一些必要的初始化工作。
    gtk_init( &argc , &argv );
    // gtk_window_new() : 创建一个窗口并返回这个窗口的控件指针
    // GTK_WINDOW_TOPLEVEL : 指明窗口的类型为最上层的主窗口
    // GtkWidget * : GtkWidget是GTK+控件类型，GtkWidget * 能指向任何控件的指针类型
    GtkWidget *window = gtk_window_new( GTK_WINDOW_TOPLEVEL );
    //gtk_widget_show() : 显示窗口控件window
    gtk_widget_show( window );

    //gtk_main()是在每个Gtk应用程序都要调用的函数
    // 程序运行停在这里等待事件(如键盘事件或鼠标事件)的发生，等待用户来操作窗口
    gtk_main();
    // 返回值，若为0则表示运行成功
    return 0;
}
```

---

## 参考文档

[GTK入门学习：一个简单的空白窗口](https://blog.csdn.net/tennysonsky/article/details/42708085)

