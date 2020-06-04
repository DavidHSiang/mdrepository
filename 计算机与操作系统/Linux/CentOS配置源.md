---
title: CentOS 配置源
date: 2020-04-11 14:09:36
tags: 
	- Linux 
categories: 
    - [操作系统,Linux,配置]
---

转载自：https://developer.aliyun.com/mirror/centos?spm=a2c6h.13651102.0.0.3e221b11fet6fP

---

## 简介

CentOS，是基于 Red Hat Linux 提供的可自由使用源代码的企业级 Linux 发行版本；是一个稳定，可预测，可管理和可复制的免费企业级计算平台。

<!--more-->

## 配置方法

### 1. 备份

```
mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup
```

### 2. 下载新的 CentOS-Base.repo 到 /etc/yum.repos.d/

**CentOS 6**

```
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-6.repo
```

或者

```
curl -o /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-6.repo
```

**CentOS 7**

```
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
```

或者

```
curl -o /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
```

**CentOS 8**

```
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-8.repo
```

或者

```
curl -o /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-8.repo
```

### 3. 运行 yum makecache 生成缓存

### 4. 其他

非阿里云ECS用户会出现 Couldn't resolve host 'mirrors.cloud.aliyuncs.com' 信息，不影响使用。用户也可自行修改相关配置: eg:

```
sed -i -e '/mirrors.cloud.aliyuncs.com/d' -e '/mirrors.aliyuncs.com/d' /etc/yum.repos.d/CentOS-Base.repo
```

## 相关链接

- 下载地址: https://mirrors.aliyun.com/centos/
  https://mirrors.aliyun.com/centos-vault/
- 官方主页: http://www.centos.org/
- 邮件列表: http://www.centos.org/modules/tinycontent/index.php?id=16
- 论坛: http://www.centos.org/modules/newbb/
- 文档: http://www.centos.org/docs/
- Wiki: http://wiki.centos.org/