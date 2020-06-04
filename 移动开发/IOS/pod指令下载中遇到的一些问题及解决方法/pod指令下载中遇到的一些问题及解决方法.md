---
title: pod指令下载中遇到的一些问题及解决方法
date: 2020-05-18 12:38:36
reward: true
declare: true
tags: 
	- IOS
categories: 
	- [移动开发,IOS]
---

## 一、报错 [!] CDN: trunk Repo update failed

> 解决办法：

### 1.podfile文件中指定source源为master：

```bash
source 'https://github.com/CocoaPods/Specs.git'
```

### 2.移除trunk源

执行`pod repo remove trunk`移除trunk源。执行完后，`pod search`就都正常了！

<!--more-->

## 二、卡在从github复制cocoapods

> 卡在:

```bash
Cloning spec repo `cocoapods` from `git@github.com:CocoaPods/Specs.git`
```

> 解决办法：

```bash
pod setup
cd ~/.cocoapods/repos 
git clone --depth 1 https://github.com/CocoaPods/Specs.git master
```

> 如果报错：

```bash
error: RPC failed; curl 18 transfer closed with outstanding read data remaining 
fatal: The remote end hung up unexpectedly
fatal: early EOF
fatal: index-pack failed
```

> 解决方法：

```bash
git config --global http.postBuffer 524288000
```

## 三、从本地库下载

使用如下语句, pod会先从本地库下载。若本地没有, 再去远程库下载

```bash
pod install --verbose --no-repo-update
pod update --verbose --no-repo-update
```

## 参考文档

[Cloning spec repo \`cocoapods\` from \`git@github.com:CocoaPods/Specs.git\`](https://www.jianshu.com/p/2f72345581e0) : https://www.jianshu.com/p/2f72345581e0

[[!] CDN: trunk Repo update failed](https://www.jianshu.com/p/bf1cbe49cb5d) : https://www.jianshu.com/p/bf1cbe49cb5d