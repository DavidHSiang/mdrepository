---
title: Redis学习笔记(四)-Redis常用命令
date: 2020-05-30 21:24:36
reward: true
declare: true
tags: 
	- Redis
categories: 
	- [数据库,Redis]
---

## 一、Redis命令

### (1)简介

Redis命令用于在redis服务上执行操作, 要在redis服务上执行命令需要一个 redis 客户端(redis-cli)

Redis支持五种数据类型:

* string 字符串
* hash 哈希
* list 列表
* set 集合
* zset (sorted set) 有序集合

### (2)客户端相关命令

> 客户端登录命令

```bash
$ redis-cli -h host -p port -a password
```

> 检测 redis 服务是否启动

```bash
$redis-cli
redis 127.0.0.1:6379>
redis 127.0.0.1:6379> PING

PONG
```

<!--more-->

## 二、key管理

### (1)常用命令

| 命令                         | 含义                                                         |
| ---------------------------- | ------------------------------------------------------------ |
| ``set key value``            | 设置一个键值对                                               |
| ``get key``                  | 根据键得到值                                                 |
| ``type key``                 | 返回 key 所储存的值的类型                                    |
| ``keys pattern``             | 根据条件``pattern``进行查询, 返回满足条件的所有键<br>例如: <br>``key *`` 查询所有<br/>``abc*``查询所有``abc``开头的键 |
| ``exists key``               | 检查给定 key 是否存在<br>存在返回1, 不存在返回0              |
| ``expire key seconds``       | 为给定 key 设置过期时间，以秒计                              |
| ``del key``                  | key 存在时删除  key                                          |
| ``ttl key``                  | 以秒为单位，返回给定 key 的剩余生存时间(TTL, time to live)<br> 当key不存在时, 返回 -2<br>存在但没有设置剩余生存时间时, 返回 -1 |
| ``pttl key``                 | 以毫秒为单位返回 key 的剩余的过期时间                        |
| ``persist key``              | 移除 key 的过期时间，key 将持久保持                          |
| ``pexpire key milliseconds`` |                                                              |
| ``move key db``              | 将当前数据库的 key 移动到给定的数据库 db 当中                |
| ``randomkey``                | 从当前数据库中随机返回一个 key                               |
| ``rename key newkey``        | 修改 key 的名称                                              |
| ``echo``                     | 打印命令                                                     |
| ``dbsize``                   | 查看数据库的key数量                                          |
| ``info``                     | 查看数据库信息                                               |
| ``config get *``             | 实时传储收到的请求,返回相关的配置                            |
| ``flushdb``                  | 清空当前数据库                                               |
| ``flushall``                 | 清空所有数据库                                               |

### (2)应用场景

``expire key seconds`` 和 ``exists key``

1. 限时的优惠活动信息
2. 网站数据缓存(对于一些需要定时更新的数据,例如:积分排行榜)
3. 手机验证码
4. 限制网站访客访问频率(防止流量攻击, 例如: 3秒最多访问5次)

### (3)Key的命名建议

redis对Key的命名没有特别的限制, **redis单个key允许存入512M大小**

* key不要太长, 尽量不要超过1024字节, 这不仅消耗内存, 而且也会降低查找的效率
* key不要太短, 太短的化, key的可读性会降低
* 在一个项目中, key最好使用统一的命名模式 , 例如 : user:123:password (在redis命名中, 一般情况下, 不同的单词**使用冒号":"进行分隔**。**redis的数据与数据之间没有关联关系, 需要通过命名来表达数据之间的关联关系**)
* key名称区分大小写

## 三、String类型

### (1)简介

string类型是Redis最基本的数据类型, 一个键最大能存储512MB

string数据结构是简单的key-value类型, value不仅可以是string, 也可以是数字, 是包含多种类型的特殊类型

string类型是二进制安全的, 意思是redis的string可以包含任何数据, 比如对序列化的对象进行存储, 对一张图片进行二进制存储, 对一个简单的字符串, 数值进行存储

### (2)常用命令

| 命令                              | 含义                                                         |
| --------------------------------- | ------------------------------------------------------------ |
| ``set key value``                 | 存储一个键值对<br>若key已经存储值, 则进行覆盖且无视类型      |
| ``setnx key value``               | 存储一个键值对<br>若key不存在, 则设值, 并返回 1<br>若key存在, 这不设值, 并返回 0<br>这是解决分布式锁的方案之一 |
| ``setex key seconds value``       | 设置key的值为value<br>过期时间为seconds秒                    |
| ``setrange key offset value``     | 指定的字符串覆盖给定 key 所储存的字符串值<br>覆盖的位置从偏移量 offset 开始 |
| ``get key``                       | 获取key的值<br>若key不存在, 返回 nil<br>若key的值的类型不是字符串, 返回一个错误 |
| ``getrange key start end``        | 获取key中字符串的子字符串<br>字符串从start开始, end结束(包括 start 和end ) |
| ``getbit key offset``             | 对 key 所储存的字符串值, 获取指定偏移量上的位(bit)           |
| ``getset key value``              | 将给定 key 的值设为 value , 并返回 key 的旧值(old value)<br>当 key 不存在时, 返回 nil |
| ``strlen key``                    | 对 key 所储存的字符串值的长度                                |
| ``del key [key...]``              | 删除指定的key , 返回被删除 key 的数量                        |
| ``mset key value [key value...]`` | 批量写, 例如: <br/>mset k1 v1 k2 v2 ...                      |
| ``mget key [key ...]``            | 批量读, 例如<br/>mget k1 k2 k3 ...                           |
| ``incr key``                      | 自增, key中存储的数字值自增1<br/>若key不存在, key的值先被初始化为0, 再执行incr操作 |
| ``decr key``                      | 自减, key中存储的数字值自减1<br/>若key不存在, key的值先被初始化为0, 再执行decr操作 |
| ``incrby key increment``          | 根据增量值自增<br/>key中存储的数字值自增 increment <br/>若key不存在, key的值先被初始化为0, 再执行incrby操作 |
| ``decrby key decrement``          | 根据增量值自减<br/>key中存储的数字值自减 decrement <br/>若key不存在, key的值先被初始化为0, 再执行decrby操作 |
| ``append key value``              | 若 key 已存在且为字符串, 将value追加到key原来值的末尾<br/>若 key 不存在, 将给定 key 设为 value |

### (3)应用场景

1. String通常用于保存单个字符串或JSON字符串数据
2. 因String是二进制安全的, 所以完全可以把一个图片文件的内容作为字符串来存储
3. 计数器(常规key-value缓存应用, 常规计数:微博数、粉丝数、点赞数...)

> INCR等指令本身就具有**原子性**, 所以我们完全可以利用redis的``incr``、``incrby``、``decr``、``decrby``等指令来实现原子计数的效果。例如: 有多个客户端同时读取了num值(值为2, 获取点赞数), 然后同时对其进行了加1操作(点赞), 那么, 最后num的值一定为 5

## 四、Hash类型

### (1)简介

​		hash类型是String类型的field(字段)和value(值)的映射表。hash特别适合用于**存储对象**, 将一个对象类型存储在hash类型比存储在String类型(JSON)占用的内存空间更少。Redis中每个hash可以存储 2的32次方 - 1 键值对

### (2)常用命令

| 命令                                        | 含义                                                  |
| ------------------------------------------- | ----------------------------------------------------- |
| ``hset key field value``                    | 将哈希表 key 中的字段 field 的值设为 value            |
| ``hmset key field value [field value ...]`` | 同时将多个 field-value (域-值)对设置到哈希表 key 中   |
| ``hget key field``                          | 获取存储在哈希表中指定字段的值                        |
| ``hmget key field [field ...]``             | 获取所有给定字段的值                                  |
| ``hgetall key``                             | 获取哈希表 key 中的所有字段和值                       |
| ``hkeys key``                               | 获取哈希表 key 中的所有字段                           |
| ``hlen key``                                | 获取哈希表 key 中字段的数量                           |
| ``hdel key field [field ...]``              | 删除哈希表 key 中一个或多个字段                       |
| ``hsetnx key field value``                  | 只有在字段 field 不存在时，设置哈希表字段的值         |
| ``hincrby key field increment``             | 为哈希表 key 中的指定字段的整数值加上增量 increment   |
| ``hincrbyfloat key field increment``        | 为哈希表 key 中的指定字段的浮点数值加上增量 increment |
| ``hexists key field``                       | 查看哈希表 key 中，指定的字段是否存在                 |

### (3)应用场景

Hash的应用场景:

* 常用于存储一个对象

