---
title: CentOS上gcc安装
date: 2020-04-11 13:55:36
tags: 
	- C/C++
categories: 
    - [后端语言,C/C++,环境搭建]
---

转载自：https://www.jianshu.com/p/a79bdb6ed92c

---

## 一、yum安装

```swift
yum -y install gcc  
yum -y install gcc-c++ 
// 我这里执行后gcc版本是4.8,通常使用的场景都会需要指定gcc版本
```

[https://www.linuxidc.com/Linux/2016-08/133915.htm](https://links.jianshu.com/go?to=https%3A%2F%2Fwww.linuxidc.com%2FLinux%2F2016-08%2F133915.htm)

<!--more-->

## 二、压缩包安装

1.下载gcc压缩包

```cpp
// 下载地址： http://mirror.hust.edu.cn/gnu/gcc/
// 上传到服务器后解压缩
tar -zxvf gcc-4.9.4.tar.gz
```

2.下载编译所需依赖项

```bash
cd gcc-4.9.4
./contrib/download_prerequisites 
cd ..
```

3.建立编译输出目录

```css
mkdir gcc-build-4.9.4
```

4.生成makefile文件

```bash
cd gcc-build-4.9.4
../gcc-4.9.4/configure --enable-checking=release --enable-languages=c,c++ --disable-multilib
```

5.编译

```go
// 时间有点久，1~3小时左右 PS：最好不要在编译过程中再去做别的什么事，整个过程CPU都是满载的，要是莫名终止了，后面麻烦事也不少。
make -j24 
```

6.安装

```go
make install
```

7.检查版本

```undefined
gcc -v
g++ -v
```

因为公司项目需要安装node环境，需要安装gcc，但是直接使用yum安转的gcc命令是4.8的，安装node时提示版本不够需要4.9。
 下面是我总结一下今天安装gcc出现的几个错误：
 1.在执行 ./configure --prefix=/usr/local/node/10.15.3 以后出现了一下的错误  ：

```jsx
WARNING: failed to autodetect C++ compiler version (CXX=g++)
creating icu_config.gypi
* Using ICU in deps/icu-small
WARNING: Using floating patch "tools/icu/patches/62/source/i18n/decimfmt.cpp" from "tools/icu"
creating icu_config.gypi
```

执行make之后报错：

```bash
ranlib .libs/libgmp.a
rm -fr .libs/libgmp.lax
creating libgmp.la
(cd .libs && rm -f libgmp.la && ln -s ../libgmp.la libgmp.la)
make[5]: Leaving directory `/usr/local/src/gcc-4.9.0/build/gmp'
make[4]: Leaving directory `/usr/local/src/gcc-4.9.0/build/gmp'
make[3]: Leaving directory `/usr/local/src/gcc-4.9.0/build/gmp'
make[2]: Leaving directory `/usr/local/src/gcc-4.9.0/build'
make[1]: *** [stage1-bubble] Error 2
make[1]: Leaving directory `/usr/local/src/gcc-4.9.0/build'
make: *** [all] Error 2
```

原因：c++没有安装
 解决办法：yum -y install gcc-c++
 (make执行以后暂时就不用管了，反正是需要好久，这篇文章写完都没结束)