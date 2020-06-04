---
title: Spring boot学习笔记(三)-Spring Boot 配置文件
date: 2020-04-19 18:24:36
reward: true
declare: true
tags: 
	- Spring boot
categories: 
    - [开发框架,Spring boot,Spring boot学习笔记]
---

## 一、Spring Boot 配置文件的存放

Spring Boot 配置文件存放在src/main/resources/目录下, 默认配置文件名为application

Spring Boot 支持两种格式的配置文件:

* .properties : src/main/resources/application.properties
* .yml : src/main/resources/application.yml

通常情况下,我们会采用yml格式的配置文件,因为yml格式的配置文件 配置更加方便,内容更加清晰