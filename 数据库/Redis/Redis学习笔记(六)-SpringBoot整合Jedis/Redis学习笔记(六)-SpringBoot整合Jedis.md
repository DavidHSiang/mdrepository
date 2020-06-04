---
title: Redis学习笔记(六)-SpringBoot整合Jedis
date: 2020-06-04 11:07:36
reward: true
declare: true
tags: 
	- Redis
categories: 
	- [数据库,Redis]
---

## 一、简介

​		在使用SpringBoot搭建微服务的时候, 很多时候需要用Redis来缓存一些数据 , 存储一些高频率访问的数据。SpringBoot整合Redis所常用的Redis常用客户端有三个: 

- Jedis api
- redisson
- lettuce

本文使用Jedis来实现Redis访问

<!--more-->

## 二、导入依赖

```xml
<dependency>
    <groupId>redis.clients</groupId>
    <artifactId>jedis</artifactId>
</dependency>
```

## 三、配置连接信息

在``application.yml``文件中, 配置 Redis 连接信息

```yml
spring:
  redis:
    port: 6379
    password: 123456
    host: 127.0.0.1
    jedis:
      pool:
        max-idle: 6 #最大空闲数
        max-active: 10 #最大连接数
        min-idle: 2 #最小空闲数
    timeout: 2000 #超时连接
```

## 四、编写JedisConfig

创建类: com.learning.config.jedis.JedisConfig

```java
@Configuration
public class JedisConfig {
    private Logger logger = LoggerFactory.getLogger(JedisConfig.class);

    @Value("${spring.redis.host}")
    private String host;

    @Value("${spring.redis.port}")
    private int port;

    @Value("${spring.redis.password}")
    private String password;

    @Value("${spring.redis.jedis.pool.max-idle}")
    private int maxIdle;

    @Value("${spring.redis.jedis.pool.max-active}")
    private int maxActive;

    @Value("${spring.redis.jedis.pool.min-idle}")
    private int minIdle;

    @Value("${spring.redis.timeout}")
    private int timeout;

    @Bean
    public JedisPool jedisPool(){
        JedisPoolConfig jedisPoolConfig = new JedisPoolConfig();
        jedisPoolConfig.setMaxIdle(maxIdle);
        jedisPoolConfig.setMinIdle(minIdle);
        jedisPoolConfig.setMaxTotal(maxActive);

        JedisPool jedisPool = new JedisPool(jedisPoolConfig,host,port,timeout,password);

        logger.info("JedisPool连接成功:"+ host + "\t" + port);

        return jedisPool;
    }
}
```

## 五、使用Jedis

### (1)注入 JedisPool 对象

在要使用 Jedis 的类中注入 JedisPool 对象

```java
 @Autowired
private JedisPool jedisPool;
```

JedisPool 的 Bean 对象是在``JedisConfig``类中声明的 :

```java
@Bean
public JedisPool jedisPool(){
	......
	return jedisPool;
}
```
### (2)使用Jedis

#### 1.得到 Jedis 对象

在方法中, 通过 jedisPool 对象得到 Jedis 对象

```java
//得到jedis对象
Jedis jedis = jedisPool.getResource();
```

#### 2.使用 jedis 对象操作Redis

**Redis 中有什么语法,  jedis 对象就有什么方法** , 例如查询 Key是否存在:

```java
jedis.exists("Key")
```

#### 3.关闭连接

在使用完 jedis 对象后, **一定要记得关闭连接**

```java
jedis.close();
```

### (3)实例 - Jedis操作 String 类型

通过 key 来得到 String 类型的 value

如果 Redis 中存在 key 则从Redis中获得 , 如果不存在 , 则到Mysql数据库中查找 , 再赋给Redis

```java
    public String getString(String key) {
        //得到jedis对象
        Jedis jedis = jedisPool.getResource();
        String val = null;
        //判断redis中key是否存在
        if(jedis.exists(key)){
            val = jedis.get(key);
            log.info("查询Redis中的数据");
        }else{
            val = "模拟从mysql查到的数据";
            log.info("查询mysql中的数据");
            jedis.set(key,val);
        }
        //关闭连接
        jedis.close();
        return val;
    }
```

### (4)实例 - Jedis操作 Hash 类型

通过 key 来得到 User 类型的 对象

如果 Redis 中存在 key 则从Redis中获得 , 如果不存在 , 则到Mysql数据库中查找 , 再赋给Redis

> User对象

```java
@Data
public class User implements Serializable {
    private String id;
    private String name;
    private Integer age;
}
```

> 查询方法

```java
public User selectUserById(String Id){
        String key = "user:" + Id;
    
        //得到jedis对象
        Jedis jedis = jedisPool.getResource();
    
        User resultUser = new User();
        Map<String,String> resultMap = new HashMap<String,String>();
        if(jedis.exists(key)){
            resultMap = jedis.hgetAll(key);
            log.info("从Redis中查询");
            String id = resultMap.get("id");
            String name = resultMap.get("name");
            Integer age = Integer.parseInt(resultMap.get("age"));
            resultUser.setId(id);
            resultUser.setName(name);
            resultUser.setAge(age);
        }else{
            //模拟从Mysql数据库查询到数据
            resultUser.setId(Id);
            resultUser.setName("张三");
            resultUser.setAge(20);
            resultMap.put("id",resultUser.getId());
            resultMap.put("name",resultUser.getName());
            resultMap.put("age",resultUser.getAge() + "");
            log.info("从Mysql中查询");
            jedis.hmset(key,resultMap);
        }
    
    //关闭连接
    jedis.close();
    
    return resultUser;
}
```

## 六、创建Jedis工具类

在开发中, 我们可以创建一个Jedis工具类, 来对Jedis进行进一步的封装, 让其实现更多的功能

例如 : 通过Jedis工具类来实现Jedis的获取和关闭

```java
@Component
public class JedisUtil {

    @Autowired
    private JedisPool jedisPool;

    public <T> T useJedis(Function<Jedis, T> function){
        Jedis jedis = jedisPool.getResource();
        T result = function.apply(jedis);
        jedis.close();
        return result;
    }

}
```

在此时, 在一个类中, 若想使用Jedis , 就无需再注入JedisPool对象了, 而是注入Jedis工具类

```java
    @Autowired
    private JedisUtil jedisUtil;
```

在`` jedisUtil ``的 ``useJedis()``方法中, 创建一个匿名类, 来实现功能 : 

```java
/**
* 通过 key 来得到 String 类型的 value
* 如果 Redis 中存在 key 则从Redis中获得 , 如果不存在 , 则到Mysql数据库中查找 , 再赋给Redis
*/
public String getString(String key) {

    String result = jedisUtil.useJedis(new Function<Jedis, String>() {
        @Override
        public String apply(Jedis jedis) {

            String val = null;
            //判断redis中key是否存在
            if(jedis.exists(key)){
                val = jedis.get(key);
                log.info("查询Redis中的数据");
            }else{
                val = "模拟从mysql查到的数据";
                log.info("查询mysql中的数据");
                jedis.set(key,val);
            }
            return val;
        }
    });

    return result;
}
```