---
title: Vue学习笔记(七)-Vue 循环语句
date: 2020-04-10 21:44:36
reward: true
declare: true
tags: 
	- Vue
categories: 
	- [JavaScript,Vue,Vue学习笔记]
---

### 一、``v-for``语句

在Vue中，我们可以通过``v-for``语句来迭代输出元素

### 二、``v-for``迭代数组

``v-for`` 指令需要以 **site in sites** 形式的特殊语法， sites 是源数据数组， site 是数组元素迭代的别名

<!--more-->

> [实例]()：迭代数组

```html
<div id = "app">
            <p v-for = "site in sites">{{site}}</p>
        </div>

        <script>
            var vm = new Vue({
                el: '#app',
                data:{
                    sites:["123","456","789"]
                }
            })
        </script>
```

### 三、``v-for``迭代对象

``v-for`` 指令需要以 **value in object** 形式的特殊语法， object 是源数据对象， value 是对象属性迭代的别名

> [实例]()：迭代对象

``` html
<div id = "app">
    <p v-for = "(value, key, index) in object">{{ index }}. {{ key }} : {{ value }}</p>
</div>

<script>
    var vm = new Vue({
        el: '#app',
        data:{
            object:{
                name:"myname",
                phone:"myphone"
            }
        }
    })
</script>
```

### 四、``v-for``迭代整数

``v-for`` 指令需要以 **n in number** 形式的特殊语法， number 是一个整数，n  是对整数迭代的别名

> [实例]()：迭代整数

``` html
<div id = "app">
    <p v-for = "n in 10">{{n}}</p>
</div>

<script>
    var vm = new Vue({el: '#app',})
</script>
```

-----

### 参考文档

[Vue.js 循环语句](https://www.runoob.com/vue2/vue-loop.html)

