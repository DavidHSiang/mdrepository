---
title: 使用vsftpd搭建ftp，用户无法上传文件
date: 2020-04-08 14:35:36
tags: 
    - Vsftpd
categories: 
    - [服务器相关,Vsftpd,Debug]
    - [服务器相关,Vsftpd,搭建]
---

转载自[使用vsftpd搭建ftp，用户无法上传文件](https://blog.csdn.net/sinat_34425079/article/details/78588966)

-----

### 553 Could not create file.

在centOS7上使用vsftpd搭建ftp服务器,参考了这篇博客： [CentOS7安装和配置FTP](/2020/04/08/CentOS7安装和配置FTP/) 

搭建完成之后，可以正常的进行用户登录和上传文件等操作，却不可以上传文件，一直提示553的错误。网上很多人说是防火墙导致的，然而在尝试了他们的解决方法之后，依然存在这个问题。

最后的解决方法是，集合了下面两篇文章的解决方案

[vsftp上传文件报错:553 Could not create file](/2020/04/08/vsftp%E4%B8%8A%E4%BC%A0%E6%96%87%E4%BB%B6%E6%8A%A5%E9%94%99:553%20Could%20not%20create%20file/) 

[vsftp上传文件报错:500 OOPS:vsftpd:refusing to run with writable root inside chroot ()](/2020/04/08/vsftp%E4%B8%8A%E4%BC%A0%E6%96%87%E4%BB%B6%E6%8A%A5%E9%94%99:500%20OOPS:vsftpd:refusing%20to%20run%20with%20writable%20root%20inside%20chroot%20()/) 

* 给对应用户目录提高读写权限: ``sudo chmod -R 777 [dir]``
* 修改``vsftpd.conf``,添加 ``allow_writeable_chroot=YES``

