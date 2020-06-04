---
title: jQuery学习笔记(三)-jQuery选择器
date: 2020-04-12 20:27:36
reward: true
declare: true
tags: 
	- jQuery
categories: 
    - [JavaScript,jQuery,jQuery学习笔记]
---

## 一、简介

jQuery选择器的语法类似于CSS选择器 , 用于选取符合条件的网页元素

jQuery选择器需要写在``$()``中 , ``$(selector)``返回的结果是一个jQuery对象

jQuery选择器可分为:

* 通过CSS选择器选择元素
  * 基本选择器
  * 层次选择器
  * 属性选择器
* 通过过滤选择器选择元素
  * 基本过滤选择器
  * 可见性过滤选择器

<!--more-->

## 二、基本选择器

| 选择器名   | 选择器                    | 实例              | 选取                                  |
| ---------- | :------------------------ | :---------------- | :------------------------------------ |
| 全局选择器 | *                         | $("*")            | 所有元素                              |
| id选择器   | #*id*                     | $("#idName")      | id为"idName"的元素                    |
| 类选择器   | .*class*                  | $(".className")   | 所有class为"className"的元素          |
| 并集选择器 | *selector*,*selector*,... | $(".intro,.demo") | class 为 "intro" 或 "demo" 的所有元素 |
| 标签选择器 | *element*                 | $("div")          | 所有div元素                           |

### (1)全局选择器

> 选取所有元素

```javascript
$("*")
```

### (2)id选择器

> html元素

```html
<div id="idName"></div>
```

> 选取id为"idName"的元素

```javascript
$("#idName")
```

### (3)类选择器

> html元素

```html
<div class="className"></div>
...
<div class="className"></div>
```

> 选取所有class为"className"的元素

```javascript
$(".className")
```

### (4)并集选择器

> html元素

```html
<div >...</div>
<p id="idName">...</p>
<h1 class="className"></h1>
```

> 选取所有div元素 , id为"idName"的元素 , 所有class为"className"的元素

```javascript
$("div,#idName,.className")
```

### (5)标签选择器

> html元素

```html
<div >...</div>
...
<div >...</div>
```

> 选取所有div元素

```javascript
$("div")
```

## 三、层次选择器



| 选择器名       | 选择器             | 实例         | 选取                                     |
| -------------- | ------------------ | ------------ | ---------------------------------------- |
| 子选择器       | parent > child     | $("div > p") | div 元素的直接子元素的所有 p 元素        |
| 后代选择器     | parent descendant  | $("div p")   | div 元素的后代的所有 p元素               |
| 相邻元素选择器 | element + next     | $("div + p") | 每个 div 元素相邻的下一个 p 元素         |
| 同辈元素选择器 | element ~ siblings | $("div ~ p") | 每个 div 元素**之后**的所有同级的 p 元素 |

### (1)子选择器

> html元素

```html
<div>
    <p>p1</p>
    <p>p2</p>
    <div>
    <p>p3</p>
    <p>p4</p>
	</div>
</div>
```

> 选取  div 元素的**直接子元素**的所有 p 元素 , 即p1,p2

```javascript
$("div > p")
```

### (2)后代选择器

> html元素

```html
<div>
    <p>p1</p>
    <p>p2</p>
    <div>
    <p>p3</p>
    <p>p4</p>
	</div>
</div>
```

> 选取  div 元素的后代的所有 p元素 , 即p1,p2,p3,p4

```javascript
$("div p")
```

### (3)相邻元素选择器

> html元素

```html
<div>div1</div>
<p>p1</p>
<p>p2</p>
<div>div2</div>
<p>p3</p>
<p>p4</p>
```

> 选取  每个 div 元素相邻的**下一个** p 元素, 即p1,p3

```javascript
$("div + p")
```

### (4)同辈元素选择器

> html元素

```html
<p>p1</p>
<div>div1</div>
<p>p2</p>
<p>p3</p>
<div><p>p4</p></div>
```

> 选取 每个 div 元素**之后**的所有同级的 p 元素, 即p2,p3

```javascript
$("div ~ p")
```

## 四、属性选择器

| 选择器                               | 实例                            | 选取                                                         |
| ------------------------------------ | ------------------------------- | ------------------------------------------------------------ |
| [*attribute*\]                       | $("[href\]")                    | 所有带有 href 属性的元素                                     |
| [*attribute*=*value*\]               | $("[href='default.htm'\]")      | 所有带有 href 属性且值等于 "default.htm" 的元素              |
| [*attribute*!=*value*\]              | $("[href!='default.htm'\]")     | 所有带有 href 属性且值不等于 "default.htm" 的元素            |
| [*attribute*$=*value*\]              | $("[href$='.jpg'\]")            | 所有带有 href 属性且值以 ".jpg" 结尾的元素                   |
| [*attribute*\|=*value*\]             | $("[title\|='Tomorrow'\]")      | 所有带有 title 属性且值等于 'Tomorrow' 或者以 'Tomorrow' 后跟连接符作为开头的字符串 |
| [*attribute*^=*value*\]              | $("[title^='Tom'\]")            | 所有带有 title 属性且值以 "Tom" 开头的元素                   |
| [*attribute*~=*value*\]              | $("[title~='hello'\]")          | 所有带有 title 属性且值包含单词 "hello" 的元素               |
| [*attribute**=*value*\]              | $("[title*='hello'\]")          | 所有带有 title 属性且值包含字符串 "hello" 的元素             |
| [*name*=*value*\][*name2*=*value2*\] | $( "input[id\][name$='man'\]" ) | 带有 id 属性，并且 name 属性以 man                           |

## 五、基本过滤选择器

| 选择器 | 实例         | 选取                                                         |
| ------ | ------------ | ------------------------------------------------------------ |
| :first | $("p:first") | 第一个 p元素                                                 |
| :last  | $("p:last")  | 最后一个 p元素                                               |
| :even  | $("tr:even") | 所有偶数 tr元素，索引值从 0 开始，<br/>第一个元素是偶数 (0)，第二个元素是奇数 (1)，以此类推。 |
| :odd   | $("tr:odd")  | 所有奇数 tr元素，索引值从 0 开始，<br>第一个元素是偶数 (0)，第二个元素是奇数 (1)，以此类推。 |
| :eq(*index*)    | $("ul li:eq(3)")       | 列表中的第四个元素（index 值从 0 开始） |
| :gt(*no*)       | $("ul li:gt(3)")       | 列举 index 大于 3 的元素                |
| :lt(*no*)       | $("ul li:lt(3)")       | 列举 index 小于 3 的元素                |
| :not(*selector*) | $("input:not(:empty)") | 所有不为空的输入元素                    |
| :header     | $(":header")   | 所有标题元素 h1, h2 ... |
| :animated | $(":animated") | 所有动画元素                |
| :focus    | $(":focus")    | 当前具有焦点的元素          |

## 六、可见性过滤选择器

| 选择器   | 实例               | 选取             |
| -------- | ------------------ | ---------------- |
| :hidden  | $("p:hidden")      | 所有隐藏的 p元素 |
| :visible | $("table:visible") | 所有可见的表格   |

## 参考文档

[jQuery 选择器](https://www.runoob.com/jquery/jquery-ref-selectors.html)