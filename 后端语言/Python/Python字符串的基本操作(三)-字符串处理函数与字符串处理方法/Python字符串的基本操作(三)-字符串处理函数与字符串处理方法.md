---
title: Python字符串的基本操作(三)-字符串处理函数与字符串处理方法
date: 2020-04-30 17:16:36
reward: true
declare: true
tags: 
	- Python
categories: 
	- [后端语言,Python]
---

## 字符串处理函数

|   函数及使用   |                 描述                  |
| :------------: | :-----------------------------------: |
|     len(x)     |           返回字符串x的长度           |
|     str(x)     |      将任意类型转换为字符串类型       |
| hex(x)或oct(x) | 整数x的十六进制或八进制小写形式字符串 |
|     chr(u)     |      将Unicode码转换为对应的字符      |
|     ord(x)     |      将字符转换为对应的Unicode码      |

<!--more-->

## 字符串处理方法

|          方法及使用          | 描述                                                         |
| :--------------------------: | ------------------------------------------------------------ |
|   str.lower()或str.upper()   | 返回字符串的副本,全部字符转为小写/大写                       |
|     str.split(sep=None)      | 返回一个列表,有str根据sep被分割的部分组成                    |
|        str.count(sub)        | 返回子串sub在str中出现的次数                                 |
|     str.replace(old,new)     | 返回字符串的副本, 所有old子串被替换为new                     |
| str.center(width[,fillchar]) | 字符串str根据宽度width居中, 根据fillchar填充,fillchar默认为空格 |
|       str.strip(chars)       | 从str中去掉在其左侧和右侧chars中列出的字符                   |
|        str.join(iter)        | 在iter变量除最后一个元素, 每个元素后增加一个str              |

