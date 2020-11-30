---
title: kali 下安装pocsuite3
category: 
- 渗透测试
tags: 
- Kali
- Tools
- Pocsuite3
---

## Pocsuite3简介

Pocsuite是由知道创宇404实验室打造的一款开源的远程漏洞测试框架。它是知道创宇安全研究团队发展的基石，是团队发展至今一直维护的一个项目，保障了我们的Web安全研究能力的领先。

你可以直接使用Pocsuite进行漏洞的验证与利用；你也可以基于Pocsuite进行PoC/Exp的开发，因为它也是一个PoC开发框架；同时，你还可以在你的漏洞测试工具里直接集成Pocsuite，它也提供标准的调用类。

Pocsuite3是完全由Python3编写，支持Windows/Linux/Mac OSX等系统，在原Pocsuite的基础上进行了整体的重写与升级，使整个框架更具有操作性和灵活性。

## 下载

### Pip安装

安装有两种，pip和直接运行源码。

```
pip3 install -U pocsuite3 --no-cache-dir
```

将使用Pocsuite3最新版。

## 执行：

```
pocsuite -h
```

### 检验安装效果。

![image-20201125223521825](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201125223521825.png)

## 常见安装问题解决

### 报错：

`Could not install packages due to an EnvironmentError: HTTPSConnectionPool(host='pypi.org', port=443): Read timed out.`

### 解决方案：

`sudo pip install --default-timeout=100 future`

## 使用帮助

```
pocsuite -h
```

![image-20201125223442441](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201125223442441.png)

### [官网教程](https://pocsuite.org/)

<!-- more -->

