---
title: Ubuntu下安装JDK
date: 2020-04-16 17:05:36
tags: 
	- Java
categories: 
    - [后端语言,Java]
---

转载自: https://www.jianshu.com/p/ddf1195e6d9f

---

## 一、安装默认的JRE / JDK

要安装此版本，请先更新软件包索引：

```shell
sudo apt update
```

接下来，检查Java是否安装:

```shell
java -version
```

如果Java当前未安装，您将看到以下输出:

```dart
Command 'java' not found, but can be installed with:

apt install openjdk-11-jre-headless
apt install default-jre            
apt install openjdk-8-jre-headless 
```

执行以下命令来安装OpenJDK:

```shell
sudo apt install default-jre
```

该命令将安装Java运行时环境(JRE)。这将允许你运行几乎所有的Java软件。

验证安装:

```shell
java -version
```

<!--more-->

你将看到以下输出:

```css
openjdk version "11.0.1" 2018-10-16
OpenJDK Runtime Environment (build 11.0.1+13-Ubuntu-3ubuntu3.18.10.1)
OpenJDK 64-Bit Server VM (build 11.0.1+13-Ubuntu-3ubuntu3.18.10.1, mixed mode, sharing)
```

除了JRE之外，您可能还需要Java开发工具包（JDK）才能编译和运行一些特定的基于Java的软件。 要安装JDK，请执行以下命令，该命令也将安装JRE：

```shell
sudo apt install default-jdk
```

通过检查Java编译器javac的版本来验证是否安装了JDK：

```shell
javac -version
```

您将看到以下输出：

```shell
javac 11.0.1
```

## 二、安装 OpenJDK 8

Java 8是目前的长期支持版本，虽然公共维护在2019年1月结束，但仍然得到广泛支持。要安装OpenJDK 8，请执行以下命令：



```shell
sudo apt install openjdk-8-jdk
```

验证安装:



```shell
sudo update-alternatives --config java
```

你会看到如下输出:



```cpp
  Selection    Path                                            Priority   Status
------------------------------------------------------------
* 0            /usr/lib/jvm/java-11-openjdk-amd64/bin/java      1111      auto mode
  1            /usr/lib/jvm/java-11-openjdk-amd64/bin/java      1111      manual mode
  2            /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java   1081      manual mode
```

## 三、安装OpenJDK 10/11

Ubuntu的存储库包含一个安装Java 10或11的软件包。在2018年9月之前，该软件包将安装OpenJDK 10.一旦Java 11发布，该软件包将安装Java 11。

要安装OpenJDK 10/11，请执行以下命令：



```shell
sudo apt install openjdk-11-jdk
```

要仅安装JRE，请使用以下命令：



```shell
sudo apt install openjdk-11-jre
```

接下来，让我们看看如何安装Oracle的官方JDK和JRE。

## 四、安装Oracle的官方JDK和JRE

如果您想安装由Oracle发布的正式版本Oracle JDK，则需要为要使用的版本添加新的软件包存储库。

要安装作为最新LTS版本的Java 8，请首先添加其软件包存储库：



```shell
sudo add-apt-repository ppa:webupd8team/java
```

当您添加存储库时，您会看到类似这样的消息：



```kotlin
 Oracle Java (JDK) Installer (automatically downloads and installs Oracle JDK8). There are no actual Java files in this PPA.

Important -> Why Oracle Java 7 And 6 Installers No Longer Work: http://www.webupd8.org/2017/06/why-oracle-java-7-and-6-installers-no.html

Update: Oracle Java 9 has reached end of life: http://www.oracle.com/technetwork/java/javase/downloads/jdk9-downloads-3848520.html

The PPA supports Ubuntu 18.10, 18.04, 16.04, 14.04 and 12.04.

More info (and Ubuntu installation instructions):
- http://www.webupd8.org/2012/09/install-oracle-java-8-in-ubuntu-via-ppa.html

Debian installation instructions:
- Oracle Java 8: http://www.webupd8.org/2014/03/how-to-install-oracle-java-8-in-debian.html

For Oracle Java 11, see a different PPA -> https://www.linuxuprising.com/2018/10/how-to-install-oracle-java-11-in-ubuntu.html
 More info: https://launchpad.net/~webupd8team/+archive/ubuntu/java
Press [ENTER] to continue or Ctrl-c to cancel adding it.
```

按ENTER继续。 然后更新你的软件包列表：

```shell
sudo apt update
```

包列表更新后，安装Java 8：

```shell
sudo apt install oracle-java8-installer
```

您的系统将从Oracle下载JDK并要求您接受许可协议。 接受协议并安装JDK。

现在让我们看看如何选择您想要使用的Java版本。

## 五、管理Java

您可以在一台服务器上安装多个Java。您可以使用update-alternatives命令配置哪个版本是命令行上使用的默认版本。

```shell
sudo update-alternatives --config java
```

如果您已经在本教程中安装了所有版本的Java，则输出结果如下所示：

```rust
$ There are 3 choices for the alternative java (providing /usr/bin/java).

  Selection    Path                                            Priority   Status
------------------------------------------------------------
* 0            /usr/lib/jvm/java-11-openjdk-amd64/bin/java      1111      auto mode
  1            /usr/lib/jvm/java-11-openjdk-amd64/bin/java      1111      manual mode
  2            /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java   1081      manual mode
  3            /usr/lib/jvm/java-8-oracle/jre/bin/java          1081      manual mode

Press <enter> to keep the current choice[*], or type selection number: 
```

选择与Java版本关联的数字以将其用作默认值，或者按下ENTER以保留当前设置。

您可以为其他Java命令执行此操作，例如编译器（`javac` ）：

```shell
sudo update-alternatives --config javac
```

其他可以运行该命令的命令包括但不限于： `keytool` ， `javadoc`和`jarsigner` 。

## 六、设置 JAVA_HOME 环境变量

许多使用Java编写的程序使用JAVA_HOME环境变量来确定Java安装位置。

要设置此环境变量，请先确定Java的安装位置。 使用update-alternatives命令：

```shell
sudo update-alternatives --config java
```

该命令显示Java的每个安装及其安装路径：

```rust
There are 3 choices for the alternative java (providing /usr/bin/java).

  Selection    Path                                            Priority   Status
------------------------------------------------------------
* 0            /usr/lib/jvm/java-11-openjdk-amd64/bin/java      1111      auto mode
  1            /usr/lib/jvm/java-11-openjdk-amd64/bin/java      1111      manual mode
  2            /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java   1081      manual mode
  3            /usr/lib/jvm/java-8-oracle/jre/bin/java          1081      manual mode

Press <enter> to keep the current choice[*], or type selection number: 
```

在这种情况下，安装路径如下所示：

- OpenJDK 11位于`/usr/lib/jvm/java-11-openjdk-amd64/bin/java`
- OpenJDK 8位于`/usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java`
- Oracle Java 8位于`/usr/lib/jvm/java-8-oracle/jre/bin/java`

复制首选安装的路径。 然后用`vi`或你最喜欢的文本编辑器打开`/etc/profile` ：

在profile文件末尾加入:

```bash
export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
export PATH=$JAVA_HOME/bin:$PATH
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
```

保存之后使用命令来使其生效:

```shell
source /etc/profile
```

验证是否设置了环境变量：

```shell
echo $PATH
```

你会看到你刚刚设置的路径：

```jsx
/usr/lib/jvm/java-11-openjdk-amd64/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin
```

现在就可以安装运行在Java上的软件了，例如Tomcat，Jetty，Glassfish，Cassandra或Jenkins。