---
title: Vulhub环境搭建
category: 
- 渗透测试
tags: 
- 靶场
---

### 简介

[Vulhub](https://github.com/vulhub/vulhub/blob/master/README.zh-cn.md)是一个面向大众的开源漏洞靶场，无需docker知识，简单执行一条命令即可编译、运行一个完整的漏洞靶场镜像。

### 环境

- centos7

### 步骤

- 安装docker

```shell
sudo yum install docker
```

- 安装python3

```shell
yum install python3
pip3 install --upgrade pip
```

- 安装docker-compose

```shell
pip install docker-compose
```

- 安装unzip

```shell
yum install unzip
```

- 启动环境

```shell
wget https://github.com/vulhub/vulhub/archive/master.zip -O vulhub-master.zip
unzip vulhub-master.zip
```

- 验证环境

```shell
#关闭防护墙
#编译、启动docker镜像
systemctl stop firewalld.service
systemctl disable firewalld.service
# 进入某一个漏洞/环境的目录
cd flask/ssti

# 自动化编译环境
docker-compose build

# 启动整个环境
docker-compose up -d
#查看当前镜像
docker ps
```

输出如下：

![image-20210216205306750](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20210216205306750.png)

浏览器访问ip:port

![image-20210216205334785](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20210216205334785.png)

完成。

<!-- more -->

