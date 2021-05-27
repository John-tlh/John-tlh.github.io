---
title: sql注入学习1
category: 
- 渗透测试
tags: 
- web安全
---

1. 了解mysql常用内置函数

   [mysql5.7](https://dev.mysql.com/doc/refman/5.7/en/dynindex-function.html)

2. 使用docker搭建sqli-labs实验环境

   `docker search sqli-labs`

   `docker pull acgpiano/sqli-labs`

   `docker images`

   ![image-20201220152931478](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201220152931478.png)

   可以看到这确实存在我们刚刚拉取得image

   接着运行这个镜像：

   `docker run -dt --name sqli -p 80:80 --rm  `acgpiano/sqli-labs`

   ![image-20201220153139630](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201220153139630.png)

   启动成功。输入本机ip加端口80查看：

   ![image-20201220153322826](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201220153322826.png)

   接下来可以开始愉快的玩耍了。

<!-- more -->

这些都做完后，就开始了解常用的sql函数。没有输出就等于没学，所以鼓励大家一起动手试试：

首先进入到你的容器中，启动mysql。先查看一下当前数据库中得所有数据库：

![image-20201220154225950](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201220154225950.png)

然后进行以上这些函数的练习：

![image-20201220153732928](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/20202020image-20201220153732928.png)

给出部分练习截图。

![image-20201220154655229](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201220154655229.png)

![image-20201220160007610](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201220160007610.png)

![image-20201220161224857](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201220161224857.png)

这些都做好后，就可以继续接下来得sql注入学习啦。

如果这些能独立搞懂，就已经很不错了，对于之后学习会很有帮助。

![image-20201220163349104](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201220163349104.png)

最后把这些整理下，方便之后使用时间盲注和报错注入得学习。

```sql
and 1=2 union select 1,2,3--+
select user() regexp '^ro'
ascii(substr((select user()),1,1))=114
if(ascii(substr((select user()),1,1))=114,0,sleep(5))
updatexml(1,concat(0x7e,(select @@version),0x7e),1)
```

