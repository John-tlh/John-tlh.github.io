---
title: XSS学习03-Dom型xss
category: 
- 渗透测试
tags: 
- XSS
---

### 01Dom型xss原理

Dom型的xss效果和利用方式和反射型很像，但是有区别。区别在于Dom型的xss漏洞不需要后端参与，也就是浏览器将产生漏洞的参数直接交给js代码处理，再进行返回。因此，判断他是不是dom型xss可以查看源码，看一看这个参数的全部处理过程是否显示在源码中，如果是则是dom型的xss。

### 02实战

**预备知识**：了解哪些地方可能存在Dom型xss

同反射型xss一个道理。

常见测试**payload**：

```
<img src=a onerror=alert(1)>  //onerror很容易被过滤！
<img src=a onerror=alert(document.cookie)>  //onerror很容易被过滤！
```

**演示**

- 环境：pikahu靶场--Dom型漏洞

![image-20210118011048218](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20210118011048218.png)

- xss接收平台：`https://xsshs.cn/`

**步骤**

- 攻击者构造payload提交

- 模拟其他用户访问

- 后台查看记录

这里就不演示了，直接分析一下代码：

![image-20210118015803335](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20210118015803335.png)

核心代码在这，可以看到这里a标签里面用引号包裹的值是我们可控的。然后上面的js是这个值的处理过程，只是简单的去除、拼接、放在了href中。因此可以构造payload如下进行绕过：

```html
'>'<img src=a onerror=alert(1)>
```

### 03漏洞修复

要修复也很简单，可以把innerheml函数改成text函数。这样这个值就不会被解析成heml标签。

### 04总结

<!-- more -->