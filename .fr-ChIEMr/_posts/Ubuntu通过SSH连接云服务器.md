---
title: Ubuntu通过SSH连接云服务器
date: 2020-04-08 12:28:36
tags: 
	- 服务器相关工具
categories: 
    - [服务器相关,相关工具]
---

转载自[ubuntu16.04 SSH连接云服务器](https://blog.csdn.net/qq_23478649/article/details/78761089)

---

### 一、安装SSH的服务器端

```bash
$ sudo apt install openssh-server
```

#### 二、启动ssh-server

```bash
$ /etc/init.d/ssh restart
```

<!--more-->

### 三、确认ssh-server是否正常工作

```bash
$ netstat -tlp
tcp6 0 0 *:ssh *:* LISTEN -
```

上面这一行就说明`ssh-server`已经在运行了

### 四、通过SSH登录服务器

假设服务器的IP地址是`113.112.23.124`，登录的用户名是`name`

```bash
 $ ssh -l name 113.112.23.124
```

### 五、输入密码,连接成功

