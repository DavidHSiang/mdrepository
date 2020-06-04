---
title: 解决 vscode中GTK+头文件引用找不到
date: 2020-04-11 10:26:36
tags: 
	- C/C++
categories: 
    - [开发工具,VSCode]
    - [后端语言,C/C++,GTK+]
---

转载自：https://www.cnblogs.com/hencins/p/12205064.html

---

正在进行 GTK 学习, 但是在 vscode GTK 的头文件找不到(头文件引用底下飘红, 逼死强迫症), 影响敲字键入速度.

解决一下该问题-- **vscode中c/c++头文件引用找不到(#include errors detected)**

花了我几十分钟, 可以说相当智障了...

在 c_cpp_properties.json(就是c/c++的配置文件)里面添加 "includePath":

<!--more-->

开始提示 glib.h 找不到, 我加上了 "/usr/include/glib-2.0",

然后提示 glibconfig.h 找不到, 我加上了我的本机路径, "/usr/lib/x86_64-linux-gnu/glib-2.0/include",

再然后提示 pango/pango.h 找不到, 我发现在 "/usr/include/pango-1.0/pango/pango.h" 下有,

估计引用依赖无穷尽也, 写成 **"/usr/include/\**"** 可以**遍历里面的文件夹**

所以我直接写成如下:

```
"includePath": [
                "${workspaceFolder}/**",
                "/usr/include/**",
                "/usr/lib/x86_64-linux-gnu/**"
            ],
```

不飘红了, 大和谐...