---
title: Ubuntu下安装Maven
date: 2020-04-16 16:58:36
reward: true
declare: true
tags: 
	- Maven
categories: 
    - [开发工具,Maven]
---

本文翻译自: https://linuxize.com/post/how-to-install-apache-maven-on-ubuntu-18-04/

---

## 一、使用Apt安装Apache Maven

1.首先更新包索引：

```
sudo apt update
```

2.接下来，通过键入以下命令来安装Maven：

```
sudo apt install maven
```

3.通过运行`mvn -version`命令来验证安装：

```
mvn -version
```

输出应如下所示：

```output
Apache Maven 3.5.2
Maven home: /usr/share/maven
Java version: 10.0.2, vendor: Oracle Corporation
Java home: /usr/lib/jvm/java-11-openjdk-amd64
Default locale: en_US, platform encoding: ISO-8859-1
OS name: "linux", version: "4.15.0-36-generic", arch: "amd64", family: "unix"
```

现在，Maven已安装在您的系统上，您可以开始使用它了。

<!--more-->

## 二、使用Maven压缩包安装最新版本的Apache Maven

### (1)安装OpenJDK

Maven 3.3+需要安装JDK 1.7或更高版本。我们将安装OpenJDK，这是Ubuntu 18.04中的默认JDK

1.首先更新包索引：

```
sudo apt update
```

2.通过键入以下命令安装OpenJDK软件包：

```
sudo apt install default-jdk
```

3.通过运行以下命令来验证安装：

```
java -version
```

输出应如下所示：

```output
openjdk version "10.0.2" 2018-07-17
OpenJDK Runtime Environment (build 10.0.2+13-Ubuntu-1ubuntu0.18.04.2)
OpenJDK 64-Bit Server VM (build 10.0.2+13-Ubuntu-1ubuntu0.18.04.2, mixed mode)
```

### (2)下载Apache Maven

在撰写本文时，Apache Maven的最新版本是`3.6.0`。在继续下一步之前，请检查[Maven下载页面](https://maven.apache.org/download.cgi)以查看是否有较新的版本。

1.`/tmp`使用以下`wget`命令在目录中下载Apache Maven ：

```
wget https://www-us.apache.org/dist/maven/maven-3/3.6.0/binaries/apache-maven-3.6.0-bin.tar.gz -P /tmp
```

2.下载完成后，将存档解压缩到`/opt`目录中：

```
sudo tar xf /tmp/apache-maven-*.tar.gz -C /opt
```

为了更好地控制Maven版本和更新，我们将创建一个`maven`指向Maven安装目录的超链接：

```
sudo ln -s /opt/apache-maven-3.6.0 /opt/maven
```

以后，如果您要升级Maven安装，则只需解压缩较新的版本并更改超链接以指向最新版本即可。

### (3)设置环境变量

接下来，我们需要设置环境变量。为此，请打开文本编辑器并`maven.sh`在`/etc/profile.d/`目录内部创建一个新文件。

```
sudo vim /etc/profile.d/maven.sh
```

/etc/profile.d/maven.sh中粘贴以下配置：

```sh
export JAVA_HOME=/usr/lib/jvm/default-java
export M2_HOME=/opt/maven
export MAVEN_HOME=/opt/maven
export PATH=${M2_HOME}/bin:${PATH}
```

保存并关闭文件。该脚本将在启动Shell时获得。

使用`chmod`命令使脚本可执行：

```
sudo chmod +x /etc/profile.d/maven.sh
```

最后，使用`source`命令加载环境变量：

```
source /etc/profile.d/maven.sh
```

### (4)验证安装

要验证是否正确安装了Maven，请使用`mvn -version`将打印Maven版本的命令：

```
mvn -version
```

您应该看到类似以下的内容：

```output
Apache Maven 3.6.0 (97c98ec64a1fdfee7767ce5ffb20918da4f719f3; 2018-10-24T18:41:47Z)
Maven home: /opt/maven
Java version: 10.0.2, vendor: Oracle Corporation, runtime: /usr/lib/jvm/java-11-openjdk-amd64
Default locale: en_US, platform encoding: ISO-8859-1
OS name: "linux", version: "4.15.0-36-generic", arch: "amd64", family: "unix"
```

现在，最新版本的Maven已安装在Ubuntu系统上。

## 结语

您已经在Ubuntu 18.04上成功安装了Apache Maven。现在，您可以访问[Apache Maven](https://maven.apache.org/guides/index.html)官方[文档](https://maven.apache.org/guides/index.html)页面，并了解如何开始使用Maven。