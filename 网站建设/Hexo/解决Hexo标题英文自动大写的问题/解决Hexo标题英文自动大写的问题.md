---
title: 解决Hexo标题英文自动大写的问题
date: 2020-05-11 11:52:36
reward: true
declare: true
tags: 
	- Hexo
categories: 
	- [网站建设,Hexo]
---

## 解决方法

去主题的 css 文件中找 `text-transform` 这个属性, 将所有`text-transform` 的属性值改为None

## CSS text-transform 属性

```css
/*将标签中的英文全部转换为大写*/
text-transform:uppercase;

/*将标签中的每个英文单词的第一个字母全部转换为大写*/
text-transform:capitalize;

/*将标签中的英文全部转换为小写*/
text-transform:lowercase;

/*不改变大小写*/
text-transform:None;
```