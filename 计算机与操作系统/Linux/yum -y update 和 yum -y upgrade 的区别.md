---
title: yum -y update 和 yum -y upgrade 的区别
date: 2020-04-11 14:11:36
tags: 
	- Linux 
categories: 
    - [操作系统,Linux,使用]
---

转载自：https://blog.csdn.net/u014057054/article/details/81092362

---

## 一、测试

分别测试：``yum -y upgrade``和``yum -y update``

升级前

```bash
[root@oracle11g ~]# cat /etc/redhat-release 
CentOS Linux release 7.3.1611 (Core)
```

升级前做过简单配置文件修改

### (1) yum -y upgrade    升级后

```bash
[root@oracle11g ~]# cat /etc/redhat-release 
CentOS Linux release 7.5.1804 (Core) 
```

系统和软件配置不做修改

### (2) yum -y update    升级后

```bash
[root@oracle11g ~]# cat /etc/redhat-release 
CentOS Linux release 7.5.1804 (Core) 
```

系统和软件配置文件更新

<!--more-->

## 二、结论

``yum -y update``(所有都升级和改变)

* 升级所有包,系统版本和内核，改变软件设置和系统设置

``yum -y upgrade``(不变内核和设置,升级包和系统版本)

* 升级所有包和系统版本，不改变内核,软件和系统设置
  