---
title: CentOS7安装和配置FTP
date: 2020-04-08 14:39:36
tags: 
    - Vsftpd
categories: 
    - [服务器相关,Vsftpd,搭建]
---

转载自[CentOS7安装和配置FTP](https://blog.csdn.net/the_victory/article/details/52192085)

-----

### 一、安装vsftpd

```bash
#安装vsftpd
yum install -y vsftpd
#设置开机启动
systemctl enable vsftpd.service 
# 重启
service vsftpd restart
# 查看vsftpd服务的状态
systemctl status vsftpd.service
```

---

<!--more-->

### 二、 配置vsftpd.conf

```bash
#备份配置文件 
cp /etc/vsftpd/vsftpd.conf /etc/vsftpd/vsftpd.conf.bak

#执行以下命令
sed -i "s/anonymous_enable=YES/anonymous_enable=NO/g" '/etc/vsftpd/vsftpd.conf'

sed -i "s/#anon_upload_enable=YES/anon_upload_enable=NO/g" '/etc/vsftpd/vsftpd.conf'

sed -i "s/#anon_mkdir_write_enable=YES/anon_mkdir_write_enable=YES/g" '/etc/vsftpd/vsftpd.conf'

sed -i "s/#chown_uploads=YES/chown_uploads=NO/g" '/etc/vsftpd/vsftpd.conf'

sed -i "s/#async_abor_enable=YES/async_abor_enable=YES/g" '/etc/vsftpd/vsftpd.conf'

sed -i "s/#ascii_upload_enable=YES/ascii_upload_enable=YES/g" '/etc/vsftpd/vsftpd.conf'

sed -i "s/#ascii_download_enable=YES/ascii_download_enable=YES/g" '/etc/vsftpd/vsftpd.conf'

sed -i "s/#ftpd_banner=Welcome to blah FTP service./ftpd_banner=Welcome to FTP service./g" '/etc/vsftpd/vsftpd.conf'

#添加下列内容到vsftpd.conf末尾
use_localtime=YES
listen_port=21
chroot_local_user=YES
idle_session_timeout=300
guest_enable=YES
guest_username=vsftpd
user_config_dir=/etc/vsftpd/vconf
data_connection_timeout=1
virtual_use_local_privs=YES
pasv_min_port=10060
pasv_max_port=10090
accept_timeout=5
connect_timeout=1
```

---

### 三、建立用户文件

```bash
#第一行用户名，第二行密码，不能使用root为用户名
vi /etc/vsftpd/virtusers
chris
123456
chang
123456
```

---

### 四、生成用户数据文件

```bash
db_load -T -t hash -f /etc/vsftpd/virtusers /etc/vsftpd/virtusers.db

#设定PAM验证文件，并指定对虚拟用户数据库文件进行读取

chmod 600 /etc/vsftpd/virtusers.db 
```

---

### 五、修改/etc/pam.d/vsftpd文件

```bash
# 修改前先备份 

cp /etc/pam.d/vsftpd /etc/pam.d/vsftpd.bak

# 将auth及account的所有配置行均注释掉
vi /etc/pam.d/vsftpd

auth sufficient /lib64/security/pam_userdb.so db=/etc/vsftpd/virtusers

account sufficient /lib64/security/pam_userdb.so db=/etc/vsftpd/virtusers

# 如果系统为32位，上面改为lib
```

---

### 六、新建系统用户vsftpd，用户目录为/home/vsftpd

```bash
#用户登录终端设为/bin/false(即：使之不能登录系统)
useradd vsftpd -d /home/vsftpd -s /bin/false
chown -R vsftpd:vsftpd /home/vsftpd
```

---

### 七、建立虚拟用户个人配置文件

```bash
mkdir /etc/vsftpd/vconf
cd /etc/vsftpd/vconf

#这里建立两个虚拟用户配合文件
touch chris chang

#建立用户根目录
mkdir -p /home/vsftpd/chris/

#编辑chris用户配置文件，内容如下，其他用户类似
vi chris

local_root=/home/vsftpd/chris/
write_enable=YES
anon_world_readable_only=NO
anon_upload_enable=YES
anon_mkdir_write_enable=YES
anon_other_write_enable=YES
```

---

### 八、防火墙设置

```bash
vi /etc/sysconfig/iptables
#编辑iptables文件，添加如下内容，开启21端口
-A INPUT -m state --state NEW -m tcp -p tcp --dport 21 -j ACCEPT
```

---

### 九、重启vsftpd服务器

```bash
service vsftpd restart
```

---

### 十、使用xftp等软件连接测试