---
title: Ubuntu下安装Nginx
date: 2020-04-08 12:42:36
reward: true
declare: true
tags: 
	- Nginx
categories: 
    - [服务器相关,Nginx]
---

###  一、检查/安装相关依赖

首先使用dpkg命令查看自己需要的软件是否安装

```bash
dpkg -l | grep libname
```

解决依赖包openssl安装，命令：

```bash
sudo apt-get install openssl libssl-dev
```

解决依赖包pcre安装，命令：

```bash
sudo apt-get install libpcre3 libpcre3-dev
```

解决依赖包zlib安装，命令：

```bash
sudo apt-get install zlib1g-dev
```

---

<!--more-->

### 二、下载并安装nginx

```bash
# 下载nginx安装包，官网：http://nginx.org/en/download.html
sudo wget http://nginx.org/download/nginx-1.16.1.tar.gz
# 将安装包移动至 /usr/local/src 目录下
sudo mv nginx-1.16.1.tar.gz /usr/local/src
# 加载 /usr/local/src 目录
cd /usr/local/src
# 解压安装包
sudo tar zxvf nginx-1.16.1.tar.gz
# 进入解压后的文件夹 nginx-1.16.1
cd nginx-1.16.1/
# 设置配置信息
# 若不加sudo会报错，error: C compiler cc is not found
sudo ./configure --prefix=/usr/local/nginx
# 编译
sudo make
# 安装
sudo make install
# 加载 nginx 所在文件夹
cd /usr/local/nginx/
# 启动 nginx (需加sudo权限)
sudo ./sbin/nginx
```

---

### 	三、解决 80 端口被占用

当使用``sudo ./sbin/nginx``启动 nginx 时，若 80 端口此时被占用，则会出现报错

```bash
nginx: [emerg] bind() to 0.0.0.0:80 failed (98: Address already in use)
nginx: [emerg] bind() to 0.0.0.0:80 failed (98: Address already in use)
nginx: [emerg] bind() to 0.0.0.0:80 failed (98: Address already in use)
nginx: [emerg] bind() to 0.0.0.0:80 failed (98: Address already in use)
nginx: [emerg] bind() to 0.0.0.0:80 failed (98: Address already in use)
nginx: [emerg] still could not bind()
```

解决方法是，查看占用 80 端口的进程，并把他删除(确保该进程不需要使用了)

```bash
# 查看占用 80 端口的进程
sudo netstat -antp
```

| Proto | Recv-Q | Send-Q | Local Address | Foreign Address | State  | PID/Program name    |
| ----- | ------ | ------ | ------------- | --------------- | ------ | ------------------- |
| tcp   | 0      | 0      | 0.0.0.0:80    | 0.0.0.0:*       | LISTEN | 12350/nginx: master |

```bash
# 杀死进程12350
sudo kill -9 12350
```

---

### 参考文档

[linux下解决80端口被占用](https://blog.csdn.net/qq_33421902/article/details/80237266)

[ubuntu下安装nginx时依赖库zlib，pcre，openssl安装方法](https://blog.csdn.net/z920954494/article/details/52132125)

[linux下安装nginx error: the HTTP rewrite module requires the PCRE library.](https://blog.csdn.net/hybaym/article/details/50929958)