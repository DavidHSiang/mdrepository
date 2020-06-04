---
title: jQuery学习笔记(二)-jQuery基本语法
copyright: true
date: 2020-04-10 22:13:36
reward: true
declare: true
tags: 
	- jQuery
categories: 
	- [JavaScript,jQuery,jQuery学习笔记]
---

## 一、 基本语法

基础语法：`` $(selector).action()``

* $ : 定义 jQuery。是jQuery的简洁写法 , 当$符与其他框架的语法冲突时,可用**jQuery**来代替
* (selector) : 选择器。通过选择器,选取 HTML 元素,选择器的语法与css选择器语法相似
* action(): 执行对元素的操作

<!--more-->

## 二、文档就绪事件(入口函数)

在实例中的所有 jQuery 函数位于一个``$(document).ready()``函数中：

```javascript
$(document).ready(function(){    
    // 开始写 jQuery 代码... 
});
```

这是为了防止文档在完全加载（就绪）之前运行 jQuery 代码，即在 DOM 加载完成后才可以对 DOM 进行操作。

如果在文档没有完全加载之前就运行函数，操作可能失败。下面是两个具体的例子：

- 试图隐藏一个不存在的元素
- 获得未完全加载的图像的大小

> 简洁写法

```javascript
$(function(){
    // 开始写 jQuery 代码... 
});
```

> 简洁写法2 - 使用箭头函数代替function()

```javascript
$(()=>{
    // 开始写 jQuery 代码... 
});
```

以上三种方式你可以选择你喜欢的方式实现文档就绪后执行 jQuery 方法

## 三、jQuery 入口函数与JavaScript 入口函数的区别

jQuery 入口函数:

```javascript
$(document).ready(function(){
    // 执行代码
});
//或者
$(function(){
    // 执行代码
});
//或者
$(()=>{
    // 执行代码
});
```

JavaScript 入口函数:

```js
window.onload = function () {
    // 执行代码
}
```

jQuery 入口函数与 JavaScript 入口函数的区别：

- jQuery 的入口函数是在 html 所有标签(DOM)都加载之后，就会去执行。
- JavaScript 的 ``window.onload`` 事件是等到所有内容，包括外部图片之类的文件加载完后，才会执行。

![jQuery入口函数和JS入口函数的区别](img/jQuery入口函数和JS入口函数的区别.jpeg)