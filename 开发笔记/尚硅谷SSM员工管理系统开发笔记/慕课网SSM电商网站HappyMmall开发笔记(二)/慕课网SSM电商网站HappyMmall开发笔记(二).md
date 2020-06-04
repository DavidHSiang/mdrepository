---
title: 慕课网SSM电商网站HappyMmall开发笔记(二)
date: 2020-05-16 22:09:36
reward: true
declare: true
tags: 
	- 慕课网SSM电商网站
categories: 
    - [开发笔记,慕课网SSM电商网站]
---

## 一、前文回顾

在笔记(一)中, 主要实现了: 数据表的设计与创建、创建Web工程、git初始化

本文主要实现了pom文件的基本配置<!--待更-->

<!--more-->


## 二、pom文件配置

### (1)配置字符集

在``pom.xml``的``<properties>``标签中, 配置``UTF-8``字符集

```xml
<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
    <maven.compiler.encoding>UTF-8</maven.compiler.encoding>
</properties>
```

### (2)配置Maven的Java版本

```xml
<properties>
    <maven.compiler.source>1.8</maven.compiler.source>
    <maven.compiler.target>1.8</maven.compiler.target>
</properties>
```

### (3)配置框架的版本

这里使用的版本是Maven中央仓库中, 最新的几个版本中使用数最多的版本。这样可以保证功能相对较新, 而遇到bug也很容易查到解决方案

最新版本可以到Maven中央仓库中进行查找: https://mvnrepository.com/

```xml
<properties>
    <org.springframework.version>5.2.4.RELEASE</org.springframework.version>
    <org.mybatis.version>3.4.6</org.mybatis.version>
    <org.mybatis.spring.version>1.3.2</org.mybatis.spring.version>
</properties>
```

### (4)导入相关依赖

#### 1.导入servlet-api

在教程中, servlet依赖使用的是tomcat-servlet-api, 而且没有使用`` <scope>provided</scope>``。这里使用的是javax.servlet-api ,  而且加上了`` <scope>provided</scope>``。

javax.servlet-api和tomcat-servlet-api内容上没太大区别, javax.servlet-api更加普遍一些。

最好使用`` <scope>provided</scope>``。如果不加一个选项。那么servlet-api会随着项目一起发布。而tomcat自带了servlet-api, 这样可能会和tomcat自带的servlet-api发生冲突。在高版本的Tomcat中 , 会用pom里配置的servlet-api , 但除非特殊的业务需求 , 这是没有必要的操作

```xml
<!-- https://mvnrepository.com/artifact/javax.servlet/javax.servlet-api -->
<dependency>
    <groupId>javax.servlet</groupId>
    <artifactId>javax.servlet-api</artifactId>
    <version>4.0.1</version>
    <scope>provided</scope>
</dependency>
```

#### 2.导入SpringMVC

```xml
<!--SpringMVC-->
<!-- https://mvnrepository.com/artifact/org.springframework/spring-webmvc -->
<dependency>
  <groupId>org.springframework</groupId>
  <artifactId>spring-webmvc</artifactId>
  <version>${org.springframework.version}</version>
</dependency>
```

#### 3.导入oxm<!--?-->

```xml
<dependency>
  <groupId>org.springframework</groupId>
  <artifactId>spring-oxm</artifactId>
  <version>${org.springframework.version}</version>
</dependency>
```

#### 4.导入Spring jdbc/事务控制 相关依赖

```xml
<!-- Spring事务控制-->
<!-- https://mvnrepository.com/artifact/org.springframework/spring-jdbc -->
<dependency>
  <groupId>org.springframework</groupId>
  <artifactId>spring-jdbc</artifactId>
  <version>${org.springframework.version}</version>
</dependency>
```

#### 5.Spring整合Junit 相关依赖

```xml
<!--Spring整合Junit-->
<!-- https://mvnrepository.com/artifact/org.springframework/spring-test -->
<dependency>
  <groupId>org.springframework</groupId>
  <artifactId>spring-test</artifactId>
  <version>${org.springframework.version}</version>
  <scope>test</scope>
</dependency>
```

#### 6.AOP相关依赖<!--?-->

```xml
<!--AOP-->
<!-- https://mvnrepository.com/artifact/org.aspectj/aspectjweaver -->
<dependency>
  <groupId>org.aspectj</groupId>
  <artifactId>aspectjweaver</artifactId>
  <version>1.9.5</version>
</dependency>

<!--AOP-->
<!-- https://mvnrepository.com/artifact/org.aspectj/aspectjrt -->
<dependency>
  <groupId>org.aspectj</groupId>
  <artifactId>aspectjrt</artifactId>
  <version>1.9.5</version>
</dependency>
```

#### 7.mybatis与mybatis整合spring

```xml
<!--mybatis整合Spring-->
<!-- https://mvnrepository.com/artifact/org.mybatis/mybatis-spring -->
<dependency>
  <groupId>org.mybatis</groupId>
  <artifactId>mybatis-spring</artifactId>
  <version>${org.mybatis.spring.version}</version>
</dependency>

<!--mybatis-->
<!-- https://mvnrepository.com/artifact/org.mybatis/mybatis -->
<dependency>
  <groupId>org.mybatis</groupId>
  <artifactId>mybatis</artifactId>
  <version>${org.mybatis.version}</version>
</dependency>
```

#### 8.Json序列化与反序列化<!--?-->

```xml
<!--Json序列化与反序列化-->
<!-- https://mvnrepository.com/artifact/org.codehaus.jackson/jackson-mapper-asl -->
<dependency>
  <groupId>org.codehaus.jackson</groupId>
  <artifactId>jackson-mapper-asl</artifactId>
  <version>1.9.13</version>
</dependency>
```

#### 9.连接池

```xml
<!--连接池-->
<!-- https://mvnrepository.com/artifact/commons-dbcp/commons-dbcp -->
<dependency>
  <groupId>commons-dbcp</groupId>
  <artifactId>commons-dbcp</artifactId>
  <version>1.4</version>
</dependency>
```

#### 10.日志

```xml
<!--日志-->
<!-- https://mvnrepository.com/artifact/ch.qos.logback/logback-classic -->
<dependency>
  <groupId>ch.qos.logback</groupId>
  <artifactId>logback-classic</artifactId>
  <version>1.2.3</version>
  <scope>compile</scope>
</dependency>
<!-- https://mvnrepository.com/artifact/ch.qos.logback/logback-core -->
<dependency>
  <groupId>ch.qos.logback</groupId>
  <artifactId>logback-core</artifactId>
  <version>1.2.3</version>
  <scope>compile</scope>
</dependency>
```

#### 11.mysql驱动

```xml
<!--mysql驱动-->
<!-- https://mvnrepository.com/artifact/mysql/mysql-connector-java -->
<dependency>
  <groupId>mysql</groupId>
  <artifactId>mysql-connector-java</artifactId>
  <version>5.1.6</version>
</dependency>
```

#### 12.guava<!--?-->

```xml
<!--guava-->
<!-- https://mvnrepository.com/artifact/com.google.guava/guava -->
<dependency>
  <groupId>com.google.guava</groupId>
  <artifactId>guava</artifactId>
  <version>28.2-jre</version>
</dependency>
```

#### 13.commons-lang3工具包<!--?-->

```xml
<!--?Commons-->
<!-- https://mvnrepository.com/artifact/org.apache.commons/commons-lang3 -->
<dependency>
  <groupId>org.apache.commons</groupId>
  <artifactId>commons-lang3</artifactId>
  <version>3.9</version>
</dependency>
```

#### 14.集合工具类<!--?-->

```xml
<!--?集合工具类-->
<!-- https://mvnrepository.com/artifact/commons-collections/commons-collections -->
<dependency>
  <groupId>commons-collections</groupId>
  <artifactId>commons-collections</artifactId>
  <version>3.2.1</version>
</dependency>
```

#### 15.单元测试

```xml
<dependency>
  <groupId>junit</groupId>
  <artifactId>junit</artifactId>
  <version>4.12</version>
  <scope>test</scope>
</dependency>
```

#### 16.时间处理jar包

```xml
<!--时间处理jar包-->
<!-- https://mvnrepository.com/artifact/joda-time/joda-time -->
<dependency>
  <groupId>joda-time</groupId>
  <artifactId>joda-time</artifactId>
  <version>2.10.5</version>
</dependency>
```

#### 17.id加密解密

```xml
<!--id加密解密-->
<!-- https://mvnrepository.com/artifact/org.hashids/hashids -->
<dependency>
  <groupId>org.hashids</groupId>
  <artifactId>hashids</artifactId>
  <version>1.0.3</version>
</dependency>
```

#### 18.上传ftp服务器

```xml
<!--ftpclient 上传ftp服务器-->
<!-- https://mvnrepository.com/artifact/commons-net/commons-net -->
<dependency>
  <groupId>commons-net</groupId>
  <artifactId>commons-net</artifactId>
  <version>3.6</version>
</dependency>
```

#### 19.文件上传

```xml
<!--file upload 文件上传-->
<!-- https://mvnrepository.com/artifact/commons-fileupload/commons-fileupload -->
<dependency>
  <groupId>commons-fileupload</groupId>
  <artifactId>commons-fileupload</artifactId>
  <version>1.3.3</version>
</dependency>
<!--文件上传相关-->
<!-- https://mvnrepository.com/artifact/commons-io/commons-io -->
<dependency>
  <groupId>commons-io</groupId>
  <artifactId>commons-io</artifactId>
  <version>2.4</version>
</dependency>
```

#### 20.Mybatis分页插件<!--?-->

```xml
<dependency>
  <groupId>com.github.pagehelper</groupId>
  <artifactId>pagehelper</artifactId>
  <version>5.1.11</version>
</dependency>

<!-- https://mvnrepository.com/artifact/com.github.miemiedev/mybatis-paginator -->
<dependency>
  <groupId>com.github.miemiedev</groupId>
  <artifactId>mybatis-paginator</artifactId>
  <version>1.2.17</version>
</dependency>

<!-- https://mvnrepository.com/artifact/com.github.jsqlparser/jsqlparser -->
<dependency>
  <groupId>com.github.jsqlparser</groupId>
  <artifactId>jsqlparser</artifactId>
  <version>3.1</version>
</dependency>
```

#### 21.alipay相关依赖

```xml
<!--alipay-->
<!-- https://mvnrepository.com/artifact/commons-codec/commons-codec -->
<dependency>
  <groupId>commons-codec</groupId>
  <artifactId>commons-codec</artifactId>
  <version>1.10</version>
</dependency>
<!-- https://mvnrepository.com/artifact/commons-configuration/commons-configuration -->
<dependency>
  <groupId>commons-configuration</groupId>
  <artifactId>commons-configuration</artifactId>
  <version>1.10</version>
</dependency>
<!-- https://mvnrepository.com/artifact/commons-lang/commons-lang -->
<dependency>
  <groupId>commons-lang</groupId>
  <artifactId>commons-lang</artifactId>
  <version>2.6</version>
</dependency>
<!-- https://mvnrepository.com/artifact/commons-logging/commons-logging -->
<dependency>
  <groupId>commons-logging</groupId>
  <artifactId>commons-logging</artifactId>
  <version>1.2</version>
</dependency>
<!-- https://mvnrepository.com/artifact/com.google.zxing/core -->
<dependency>
  <groupId>com.google.zxing</groupId>
  <artifactId>core</artifactId>
  <version>3.3.3</version>
</dependency>
<!-- https://mvnrepository.com/artifact/com.google.code.gson/gson -->
<dependency>
  <groupId>com.google.code.gson</groupId>
  <artifactId>gson</artifactId>
  <version>2.8.5</version>
</dependency>
<!-- https://mvnrepository.com/artifact/org.hamcrest/hamcrest-core -->
<dependency>
  <groupId>org.hamcrest</groupId>
  <artifactId>hamcrest-core</artifactId>
  <version>1.3</version>
</dependency>
```

#### 22.redis

```xml
<!-- https://mvnrepository.com/artifact/redis.clients/jedis -->
<dependency>
  <groupId>redis.clients</groupId>
  <artifactId>jedis</artifactId>
  <version>3.2.0</version>
</dependency>
```

### (5)添加Maven插件

#### 1.mybatis-generator反向工程插件

```xml
  <plugin>
    <groupId>org.mybatis.generator</groupId>
    <artifactId>mybatis-generator-maven-plugin</artifactId>
    <version>1.4.0</version>
    <configuration>
      <configurationFile>src/main/resources/generatorConfig.xml</configurationFile>
      <verbose>true</verbose>
      <overwrite>true</overwrite>
    </configuration>
  </plugin>
```

**注意:** mybatis-generator所在的``plugins``不能在pluginManagement标签内。要和pluginManagement标签同级别(若存在pluginManagement标签)

#### 2.Maven构建工具

```xml
<plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-compiler-plugin</artifactId>
  <version>3.8.1</version>
  <configuration>
    <source>1.8</source>
    <target>1.8</target>
    <encoding>UTF-8</encoding>
    <compilerArguments>
      <extdirs>${project.basedir}/src/main/webapp/WEB-INF/lib</extdirs>
    </compilerArguments>
  </configuration>
</plugin>
```

### (6)最终的pom.xml文件

```xml
<?xml version="1.0" encoding="UTF-8"?>

<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>org.learning</groupId>
  <artifactId>mmall</artifactId>
  <version>1.0-SNAPSHOT</version>
  <packaging>war</packaging>

  <name>mmall Maven Webapp</name>
  <!-- FIXME change it to the project's website -->
  <url>http://www.example.com</url>

  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
    <maven.compiler.encoding>UTF-8</maven.compiler.encoding>

    <maven.compiler.source>1.8</maven.compiler.source>
    <maven.compiler.target>1.8</maven.compiler.target>

    <org.springframework.version>5.2.4.RELEASE</org.springframework.version>
    <org.mybatis.version>3.4.6</org.mybatis.version>
    <org.mybatis.spring.version>1.3.2</org.mybatis.spring.version>
  </properties>

  <dependencies>
    <!--servlet-api-->
    <!-- https://mvnrepository.com/artifact/javax.servlet/javax.servlet-api -->
    <dependency>
      <groupId>javax.servlet</groupId>
      <artifactId>javax.servlet-api</artifactId>
      <version>4.0.1</version>
      <scope>provided</scope>
    </dependency>

    <!--SpringMVC-->
    <!-- https://mvnrepository.com/artifact/org.springframework/spring-webmvc -->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-webmvc</artifactId>
      <version>${org.springframework.version}</version>
    </dependency>

    <!--?-->
    <!-- https://mvnrepository.com/artifact/org.springframework/spring-oxm -->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-oxm</artifactId>
      <version>${org.springframework.version}</version>
    </dependency>

    <!-- Spring事务控制-->
    <!-- https://mvnrepository.com/artifact/org.springframework/spring-jdbc -->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-jdbc</artifactId>
      <version>${org.springframework.version}</version>
    </dependency>

    <!--Spring整合Junit-->
    <!-- https://mvnrepository.com/artifact/org.springframework/spring-test -->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-test</artifactId>
      <version>${org.springframework.version}</version>
      <scope>test</scope>
    </dependency>

    <!--AOP-->
    <!-- https://mvnrepository.com/artifact/org.aspectj/aspectjweaver -->
    <dependency>
      <groupId>org.aspectj</groupId>
      <artifactId>aspectjweaver</artifactId>
      <version>1.9.5</version>
    </dependency>

    <!--AOP-->
    <!-- https://mvnrepository.com/artifact/org.aspectj/aspectjrt -->
    <dependency>
      <groupId>org.aspectj</groupId>
      <artifactId>aspectjrt</artifactId>
      <version>1.9.5</version>
    </dependency>

    <!--mybatis整合Spring-->
    <!-- https://mvnrepository.com/artifact/org.mybatis/mybatis-spring -->
    <dependency>
      <groupId>org.mybatis</groupId>
      <artifactId>mybatis-spring</artifactId>
      <version>${org.mybatis.spring.version}</version>
    </dependency>

    <!--mybatis-->
    <!-- https://mvnrepository.com/artifact/org.mybatis/mybatis -->
    <dependency>
      <groupId>org.mybatis</groupId>
      <artifactId>mybatis</artifactId>
      <version>${org.mybatis.version}</version>
    </dependency>

    <!--Json序列化与反序列化-->
    <!-- https://mvnrepository.com/artifact/org.codehaus.jackson/jackson-mapper-asl -->
    <dependency>
      <groupId>org.codehaus.jackson</groupId>
      <artifactId>jackson-mapper-asl</artifactId>
      <version>1.9.13</version>
    </dependency>

    <!--连接池-->
    <!-- https://mvnrepository.com/artifact/commons-dbcp/commons-dbcp -->
    <dependency>
      <groupId>commons-dbcp</groupId>
      <artifactId>commons-dbcp</artifactId>
      <version>1.4</version>
    </dependency>

    <!--日志-->
    <!-- https://mvnrepository.com/artifact/ch.qos.logback/logback-classic -->
    <dependency>
      <groupId>ch.qos.logback</groupId>
      <artifactId>logback-classic</artifactId>
      <version>1.2.3</version>
      <scope>compile</scope>
    </dependency>
    <!-- https://mvnrepository.com/artifact/ch.qos.logback/logback-core -->
    <dependency>
      <groupId>ch.qos.logback</groupId>
      <artifactId>logback-core</artifactId>
      <version>1.2.3</version>
      <scope>compile</scope>
    </dependency>

    <!--mysql驱动-->
    <!-- https://mvnrepository.com/artifact/mysql/mysql-connector-java -->
    <dependency>
      <groupId>mysql</groupId>
      <artifactId>mysql-connector-java</artifactId>
      <version>5.1.6</version>
    </dependency>

    <!--?guava-->
    <!-- https://mvnrepository.com/artifact/com.google.guava/guava -->
    <dependency>
      <groupId>com.google.guava</groupId>
      <artifactId>guava</artifactId>
      <version>28.2-jre</version>
    </dependency>

    <!--?Commons-->
    <!-- https://mvnrepository.com/artifact/org.apache.commons/commons-lang3 -->
    <dependency>
      <groupId>org.apache.commons</groupId>
      <artifactId>commons-lang3</artifactId>
      <version>3.9</version>
    </dependency>

    <!--?集合工具类-->
    <!-- https://mvnrepository.com/artifact/commons-collections/commons-collections -->
    <dependency>
      <groupId>commons-collections</groupId>
      <artifactId>commons-collections</artifactId>
      <version>3.2.1</version>
    </dependency>

    <!--单元测试-->
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.12</version>
      <scope>test</scope>
    </dependency>

    <!--?时间处理jar包-->
    <!-- https://mvnrepository.com/artifact/joda-time/joda-time -->
    <dependency>
      <groupId>joda-time</groupId>
      <artifactId>joda-time</artifactId>
      <version>2.10.5</version>
    </dependency>

    <!--?id加密解密-->
    <!-- https://mvnrepository.com/artifact/org.hashids/hashids -->
    <dependency>
      <groupId>org.hashids</groupId>
      <artifactId>hashids</artifactId>
      <version>1.0.3</version>
    </dependency>

    <!--?ftpclient 上传ftp服务器-->
    <!-- https://mvnrepository.com/artifact/commons-net/commons-net -->
    <dependency>
      <groupId>commons-net</groupId>
      <artifactId>commons-net</artifactId>
      <version>3.6</version>
    </dependency>

    <!--?file upload 文件上传-->
    <!-- https://mvnrepository.com/artifact/commons-fileupload/commons-fileupload -->
    <dependency>
      <groupId>commons-fileupload</groupId>
      <artifactId>commons-fileupload</artifactId>
      <version>1.3.3</version>
    </dependency>
    <!--?文件上传相关-->
    <!-- https://mvnrepository.com/artifact/commons-io/commons-io -->
    <dependency>
      <groupId>commons-io</groupId>
      <artifactId>commons-io</artifactId>
      <version>2.4</version>
    </dependency>

    <!--?Mybatis分页插件-->
    <dependency>
      <groupId>com.github.pagehelper</groupId>
      <artifactId>pagehelper</artifactId>
      <version>5.1.11</version>
    </dependency>

    <!-- https://mvnrepository.com/artifact/com.github.miemiedev/mybatis-paginator -->
    <dependency>
      <groupId>com.github.miemiedev</groupId>
      <artifactId>mybatis-paginator</artifactId>
      <version>1.2.17</version>
    </dependency>

    <!-- https://mvnrepository.com/artifact/com.github.jsqlparser/jsqlparser -->
    <dependency>
      <groupId>com.github.jsqlparser</groupId>
      <artifactId>jsqlparser</artifactId>
      <version>3.1</version>
    </dependency>

    <!--alipay-->
    <!-- https://mvnrepository.com/artifact/commons-codec/commons-codec -->
    <dependency>
      <groupId>commons-codec</groupId>
      <artifactId>commons-codec</artifactId>
      <version>1.10</version>
    </dependency>
    <!-- https://mvnrepository.com/artifact/commons-configuration/commons-configuration -->
    <dependency>
      <groupId>commons-configuration</groupId>
      <artifactId>commons-configuration</artifactId>
      <version>1.10</version>
    </dependency>
    <!-- https://mvnrepository.com/artifact/commons-lang/commons-lang -->
    <dependency>
      <groupId>commons-lang</groupId>
      <artifactId>commons-lang</artifactId>
      <version>2.6</version>
    </dependency>
    <!-- https://mvnrepository.com/artifact/commons-logging/commons-logging -->
    <dependency>
      <groupId>commons-logging</groupId>
      <artifactId>commons-logging</artifactId>
      <version>1.2</version>
    </dependency>
    <!-- https://mvnrepository.com/artifact/com.google.zxing/core -->
    <dependency>
      <groupId>com.google.zxing</groupId>
      <artifactId>core</artifactId>
      <version>3.3.3</version>
    </dependency>
    <!-- https://mvnrepository.com/artifact/com.google.code.gson/gson -->
    <dependency>
      <groupId>com.google.code.gson</groupId>
      <artifactId>gson</artifactId>
      <version>2.8.5</version>
    </dependency>
    <!-- https://mvnrepository.com/artifact/org.hamcrest/hamcrest-core -->
    <dependency>
      <groupId>org.hamcrest</groupId>
      <artifactId>hamcrest-core</artifactId>
      <version>1.3</version>
    </dependency>

    <!-- https://mvnrepository.com/artifact/redis.clients/jedis -->
    <dependency>
      <groupId>redis.clients</groupId>
      <artifactId>jedis</artifactId>
      <version>3.2.0</version>
    </dependency>

  </dependencies>

  <build>
    <finalName>mmall</finalName>
    <plugins>
      <plugin>
        <groupId>org.mybatis.generator</groupId>
        <artifactId>mybatis-generator-maven-plugin</artifactId>
        <version>1.4.0</version>
        <configuration>
          <configurationFile>src/main/resources/generatorConfig.xml</configurationFile>
          <verbose>true</verbose>
          <overwrite>true</overwrite>
        </configuration>
      </plugin>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>3.8.1</version>
        <configuration>
          <source>1.8</source>
          <target>1.8</target>
          <encoding>UTF-8</encoding>
          <compilerArguments>
            <extdirs>${project.basedir}/src/main/webapp/WEB-INF/lib</extdirs>
          </compilerArguments>
        </configuration>
      </plugin>
    </plugins>
  </build>
</project>
```