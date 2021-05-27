---
title: XSS学习01
category: 
- 渗透测试
tags: 
- XSS
---

### 01XSS漏洞定义

XSS全称crose site script。指的是攻击者往web页面插入恶意js代码，当用户或者管理员访问页面触发时，插入的恶意代码执行，从而达到攻击者的目的。比如打cookie，获取用户的一些信息。也可以结合csrf漏洞一起使用从而实现更为严重的攻击。

### 02XSS漏洞的原理

xxx。

### 03XSS漏洞的分类

-  反射型

反射型与存储型对应来看。也就是攻击者的payload**经过前端页面发送到后端**，没有经过后端存储直接在前端页面被渲染执行。即没有这么一个存储的过程。一般出现在url中的某个参数。比如下面这种：

![image-20210116220557090](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20210116220557090.png)

- 存储型

存储型与反射型的不同在于他有后端存储的一个过程。比如将攻击者的payload存储在一个介质中，可以是数据库、文件或者缓存中。重点是他经过了存储。典型的场景如留言框：

![image-20210116220800373](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20210116220800373.png)

因为他经过了存储，所以你每次访问这个页面都会处罚攻击者的payload。

- DOM型

DOM型的xss有点像反射型xss。区别在于Dom型的xss他传递的payload**没有发送给后端接收而是由前端js处理**，也就是这种xss不需要后端参与。像这种，提交的参数由js处理然后返回数据给页面就是属于dom型的xss。

![image-20210116221521324](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20210116221521324.png)

其实从本质上来说，xss也就是两类，存储型和非存储型。

### 04XSS漏洞修复

- HTML实体编码
- 使用白名单过滤
- 根据业务场景对症下药

不管哪种都不能一劳永逸，没有说就绝对安全了。

<!-- more -->