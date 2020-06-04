---
title: Ubuntu下安装proxychains教程
date: 2020-04-08 11:32:36
reward: true
declare: true
tags: 
	- 科学上网
categories: 
    - [科学上网,SSR]
---

> 本文讲解如何在Ubuntu上安装并使用proxychains代理工具,这是基于SSR脚本启动SSR代理的必备工具

### 1. 安装

#### 1.1 编译安装

##### 1.1.0 确保ubuntu安装了C的编译器(如gcc)

```
gcc --version
```

<!--more-->

![检查GCC安装](img/检查GCC安装.png)

若未安装GCC，可参考[Ubuntu下安装gcc](/2020/04/08/Ubuntu下安装gcc/)

##### 1.1.1 下载源码包

```
git clone https://github.com/rofl0r/proxychains-ng.git
```

##### 1.1.2 进入安装目录

```
cd proxychains-ng/
```

##### 1.1.3 编译安装

```
./configure --prefix=/usr --sysconfdir=/etc
make && make install
make install-config  # 创建配置文件
```

#### 1.2 apt安装

注意apt源安装的是第3版的proxychains

```
apt-get install proxychains
```

-----

### 2. 配置proxyChains

```
vim /etc/proxychains.conf
```

将dynamic_chain前面的注释去掉，再将[ProxyList]下的socks4 改为socks5，并且127.0.0.1后面的端口改为1080

-----

### 3.proxyChains的使用

#### 3.1 测试连接

```
proxyresolv www.google.com
```

#### 3.2 运行程序

```
proxychains programe's_name
```

-----
### 参考文档
[Ubuntu系统中使用ProxyChains设置网络代理](https://www.jianshu.com/p/3f392367b41f)

[ubuntu下安装proxychains](https://blog.csdn.net/Lazybones_3/article/details/85129470)
