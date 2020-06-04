---
title: Redis学习笔记(五)-Jedis、redisson、Lettuce的对比
date: 2020-05-30 21:26:36
reward: true
declare: true
tags: 
	- Redis
categories: 
	- [数据库,Redis]
---

## 一、简介

Redis常用客户端主要有三个:

* Jedis api
  * Jedis api 在线网址 : https://tool.oschina.net/uploads/apidocs/jedis-2.1.0/redis/clients/jedis/Jedis.html
* redisson
  * redisson 官网地址 : https://redisson.org/
  * redisson github地址 : https://github.com/redisson/redisson
* lettuce
  * lettuce 官网地址 : https://lettuce.io/
  * lettuce github地址 : https://github.com/lettuce-io/lettuce-core

**在Spring boot2之后, 对redis连接的支持, 默认就采用了lettuce**

<!--more-->

## 二、概念

* Jedis : 是老牌的Redis的Java实现客户端, 提供了比较全面的Redis命令的支持
* redisson : 实现了分布式和可扩展的Java数据结构
* Lettuce : 高级Redis客户端, 用于线程安全同步, 异步和响应使用, 支持集群, sentinel, 管道和编码器

## 三、优点

* Jedis : 比较全面的提供了Redis的操作特性
* Redisson : 促使使用者对Redis的关注分离, 提供很多分布式相关操作事务, 例如: 分布式锁, 分布式集合, 可通过Redis支持延迟队列
* Lettuce : 基于Netty框架的事件驱动的通信层, 其方法调用是异步的。Lettuce的API是线程安全的, 所以可以操作单个Lettuce连接来完成各种操作

## 四、可伸缩

* Jedis : 使用阻塞的I/O, 并且方法调用都是同步的, 程序流需要等到sockets处理完I/O才能执行, 不支持异步。Jedis客户端实例不是线程安全的, 所以需要通过连接池来使用Jedis
* Redisson : 基于Netty框架的事件驱动的通信层, 其方法调用是异步的。Redisson的API是线程安全的, 所以可以操作单个Redisson连接来完成各种操作
* Lettuce : 基于Netty框架的事件驱动的通信层, 其方法调用是异步的。Lettuce的API是线程安全的, 所以可以操作单个Lettuce连接来完成各种操作。Lettuce能够支持redis4, 需要java8及以上。Lettuce是基于Netty实现的与Redis进行同步和异步操作

## 五、比较

* Jedis :直接连接Redis Server, 非线程安全, 需使用连接池为每个Jedis实例增加物理连接
* Redisson : 基于Netty连接Redis Server, 线程安全, 功能较为简单, 不支持字符串操作, 不支持排序、事务、管道、分区等Redis特性。促使使用者对Redis的关注分离,提供很多分布式相关操作事务

* Lettuce : 基于Netty连接Redis Server, 线程安全, 一个连接实例可以满足多线程环境下的并发访问, 一个连接实例不够的情况下, 可以按需增加连接实例

## 六、总结

​		**优先使用Lettuce**, 如果需要分布式锁, 分布式集合等分布式的高级特性, 添加Redisson结合使用, 因为Redisson对字符串操作的支持很差

