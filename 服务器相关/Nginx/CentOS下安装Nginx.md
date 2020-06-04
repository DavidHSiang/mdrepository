---
title: CentOS 下安装 Nginx
date: 2020-04-08 13:04:36
reward: true
declare: true
tags: 
	- Nginx
categories: 
    - [服务器相关,Nginx]
---

## 一、检查/安装相关依赖

首先使用 rpm 命令查看自己需要的软件是否安装

```bash
rpm -qa | grep libname
```

解决依赖包openssl安装，命令：

```bash
yum -y install openssl openssl-devel
```

解决依赖包pcre安装，命令：

```bash
yum -y install pcre pcre-devel
```

解决依赖包zlib安装，命令：

```bash
yum -y install zlib zlib-devel
```

一次性安装所有依赖

```bash
yum -y install make zlib zlib-devel gcc-c++ libtool openssl openssl-devel pcre pcre-devel
```

---

<!--more-->

## 二、下载并安装nginx

```bash
# 下载nginx安装包，官网：http://nginx.org/en/download.html
wget http://nginx.org/download/nginx-1.16.1.tar.gz
# 将安装包移动至 /usr/local/src 目录下
mv nginx-1.16.1.tar.gz /usr/local/src
# 加载 /usr/local/src 目录
cd /usr/local/src
# 解压安装包
tar zxvf nginx-1.16.1.tar.gz
# 进入解压后的文件夹 nginx-1.16.1
cd nginx-1.16.1/
# 设置配置信息
# 若不加sudo会报错，error: C compiler cc is not found
./configure --prefix=/usr/local/nginx
# 编译&安装
 make & make install
# 加载 nginx 所在文件夹
cd /usr/local/nginx/
# 启动 nginx (需加sudo权限)
./sbin/nginx
```

## 三、解决 80 端口被占用

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

## 四、解决主机无法访问 nginx

在 主机 访问 虚拟机 中 nginx,默认不能访问的,因为防火墙问题

解决方法：

(1) 关闭防火墙
(2) 开放访问的端口号,80 端口

```bash
# 查看开放的端口号
firewall-cmd --list-all
# 设置开放的端口号
firewall-cmd --add-service=http --permanent
firewall-cmd --add-port=80/tcp --permanent
# 重启防火墙(CentOS8)
systemctl restart firewalld.service
```