---
title: Nginx虚拟主机
date: 2020-04-08 14:20:36
reward: true
declare: true
tags: 
	- Nginx
categories: 
    - [服务器相关,Nginx]
---

## 一、基本配置

```bash
http {
	# 定义一个虚拟主机
    server {
    	# 设置监听 80 端口
        listen          80;
        # 设置主机名(域名/端口)
        server_name     www.a.com;
        # 设置日志路径
        access_log      logs/domain1.access.log main;
        # 默认请求
        location / {
            # 设置主页为 index.html
            index index.html;
            # 设置根目录为 /var/www/domain1.com/htdocs
            root  /var/www/domain1.com/htdocs;
        }
    }
}
```

---

<!--more-->

## 二、基于域名、ip、端口的配置

```bash
http {
	# 基于域名
	# 通过 www.a.com 访问
    server {
        listen          80;
        server_name     www.a.com;
        access_log      logs/domain1.access.log main;
        location / {
            index index.html;
            root  /var/www/domain1.com/htdocs;
        }
    }
	# 基于ip
	# 通过 192.168.127.1 访问
    server {
        listen          80;
        server_name      192.168.127.1 ;
        access_log      logs/domain1.access.log main;
        location / {
            index index.html;
            root  /var/www/domain1.com/htdocs;
        }
    }
    # 基于端口
	# 通过 2022端口 访问
    server {
        listen          2022;
        server_name     www.a.com;
        access_log      logs/domain1.access.log main;
        location / {
            index index.html;
            root  /var/www/domain1.com/htdocs;
        }
    }
}
```

---

## 三、更多参数说明

```bash
server {
        # Replace this port with the right one for your requirements
        # 根据你的需求改变此端口
        listen       80;  #could also be 1.2.3.4:80 也可以是1.2.3.4:80的形式
        # Multiple hostnames seperated by spaces.  Replace these as well.
        # 多个主机名可以用空格隔开，当然这个信息也是需要按照你的需求而改变的。
        server_name  star.yourdomain.com *.yourdomain.com www.*.yourdomain.com;
        #Alternately: _ *
        #或者可以使用：_ * (具体内容参见本维基其他页面)
        root /PATH/TO/WEBROOT/$host;
        error_page  404              http://yourdomain.com/errors/404.html;
        access_log  logs/star.yourdomain.com.access.log;
        location / {
            root   /PATH/TO/WEBROOT/$host/;
            index  index.php;
        }
        # serve static files directly
        # 直接支持静态文件 (爱月说：???从配置上看来不是直接支持啊～有问题有问题～)
        location ~* ^.+.(jpg|jpeg|gif|css|png|js|ico|html)$ {
            access_log        off;
            expires           30d;
        }
        location ~ .php$ {
          # By all means use a different server for the fcgi processes if you need to
          # 如果需要，你可以为不同的FCGI进程设置不同的服务信息
          fastcgi_pass   127.0.0.1:YOURFCGIPORTHERE;
          fastcgi_index  index.php;
          fastcgi_param  SCRIPT_FILENAME  /PATH/TO/WEBROOT/$host/$fastcgi_script_name;
          fastcgi_param  QUERY_STRING     $query_string;
          fastcgi_param  REQUEST_METHOD   $request_method;
          fastcgi_param  CONTENT_TYPE     $content_type;
          fastcgi_param  CONTENT_LENGTH   $content_length;
          fastcgi_intercept_errors on;
        }
        location ~ /.ht {
            deny  all;
        }
     }
```

