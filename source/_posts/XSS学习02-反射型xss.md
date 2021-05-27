---
title: XSS学习02-反射型xss
category: 
- 渗透测试
tags: 
- XSS
---

### 01反射型xss的原理

- 原理

攻击者插入xss代码，服务端接收xss代码输出到页面上，攻击者将带有xss代码的url发送给用户，用户访问即完成攻击。

![image-20210116222940123](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20210116222940123.png)

### 02实战

**预备知识**：了解哪些地方可能存在反射型xss

要知道这个，需要明白xss漏洞需要满足条件，即有输入点，并且用户可控制输入点知道这个就可以多去进行一些测试，比如搜索、分类等等模块。常见的技巧就是观察url中的参数，打开控制台查看这些参数是否可控。

常见测试**payload**：

```
<img src=a onerror=alert(1)>  //onerror很容易被过滤！
<img src=a onerror=alert(document.cookie)>  //onerror很容易被过滤！
```

**演示**

1. 环境：pikahu靶场--反射型xss漏洞（搜索处）
2. xss接收平台：`https://xsshs.cn/`

**步骤**

- 攻击者构造payload，生成恶意链接

![image-20210117223237271](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20210117223237271.png)

这里的搜索处对输入字符进行了限制，但url中的参数是没有限制的。因此我们直接修改url中的参数进行一个简单的绕过。

点击提交后，生成的恶意链接如下：

![image-20210117223522506](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20210117223522506.png)

- 模拟管理员点击链接，触发payload

在火狐中先进行登录，然后点开这个链接。模拟受攻击过程：

![image-20210117223616677](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20210117223616677.png)

接着访问恶意url

![image-20210117223659777](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20210117223659777.png)

- 后台查看管理员cookie，在chrome修改cookie为管理员的cookie，进行登录

![image-20210117224452441](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20210117224452441.png)

修改cookie进行登录：

![image-20210117224643076](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20210117224643076.png)



### 03总结

<!-- more -->