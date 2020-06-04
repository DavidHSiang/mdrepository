---
title: Spring boot学习笔记(三)-表现层的基本注解
date: 2020-04-19 18:36:36
reward: true
declare: true
tags: 
	- Spring boot
categories: 
    - [开发框架,Spring boot,Spring boot学习笔记]
---

## 一、表现层的基本示例

```java
@RestController
@RequestMapping("/hello")
public class HelloController {

    @Value("${name}")
    ...
        
    @Autowired
     ...
    @GetMapping("/say")
    public String sayHello(){
        return "Hello Spring Boot";
    }
}
```

