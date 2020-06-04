---
title: Hexo-theme-yilia异常Cannot read property 'length' of undefined
date: 2020-04-23 20:09:36
tags: 
	- Hexo
categories: 
	- [网站建设,Hexo]
---

本文转载自:

https://github.com/litten/hexo-theme-yilia/issues/668

## 错误内容:

`\layout\_partial\post\tag.ejs` 第7行抛出异常: Cannot read property 'length' of undefined

<!--more-->

## 解决方法:

将`./themes/yilia/layout/_partial/post/category.ejs`改为：

```ejs
<% if (post.categories && post.categories.length){ %>
<div class="article-category tagcloud">
	<i class="icon-book icon"></i>
	<ul class="article-tag-list">
		<% post.categories.forEach(function(tag, i){ %>
		<% if (tag.hasOwnProperty('name')){ %>
		<li class="article-tag-list-item">
			<a href="<%= config.root %><%= tag.path %>/" class="article-tag-list-link color<%= tag.name.length % 5 + 1 %>">
				<%-tag.name%></a>
		</li>
		<% } %>
		<% }) %>
	</ul>
</div>
<% } %>
```

将`./themes/yilia/layout/_partial/post/tag.ejs`改为：

```ejs
<% if (post.tags && post.tags.length){ %>
<div class="article-tag tagcloud">
	<i class="icon-price-tags icon"></i>
	<ul class="article-tag-list">
		<% post.tags.forEach(function(tag, i){ %>
		<% if (tag.hasOwnProperty('name')){ %>
		<li class="article-tag-list-item">
			<a href="javascript:void(0)" class="js-tag article-tag-list-link color<%= tag.name.length % 5 + 1 %>">
				<%-tag.name%></a>
		</li>
		<% } %>
		<% }) %>
	</ul>
</div>
<% } %>
```

