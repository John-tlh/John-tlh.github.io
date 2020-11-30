---
title: kali安装pocsuite3实战ThinkPHP远程代码执行
categories:
- 渗透测试
tags:
- kali
- docker
- pocsuite
comments: true
---

### 目的：

1. 在kali下安装docker实现快速搭建渗透靶场的目的。
2. 使用pocsuite3打造自己的Poc框架。

### 环境：

1. kali版本--Linux kali 4.19.0-kali3-amd64 #1 SMP Debian 4.19.20-1kali1 (2019-02-14)
2. $(lsb_release -cs)  n/a 

### 准备工作：

1. 虚拟机安装好kali后，确保软件源没有问题，并对kali系统进行更新。
2. 对kali下的软件进行安装更新。
3. 如果之前安装过docker，先对旧版本的docker进行卸载。

<!-- more -->

### 步骤：

1. 安装docker：

   安装docker这一步非常容易出错，网上的教程多而杂乱。这里建议大家按照docker官方给的[debian下安装docker](https://docs.docker.com/install/linux/docker-ce/debian/)给的安装教程进行安装，避免入坑。

2. 安装pocsuite3

   安装pocsuite相对来说比较简单，需要注意的是如果使用pip命令安装，记得先在kali中更新一下pip，否则会报错。这里贴一下我觉得写的不错的一篇[教学文章](https://zhuanlan.zhihu.com/p/231608767),从安装到基本使用教学都有。如果想了解pocsuite更多详细的信息请传送到[pocsuite官网](https://pocsuite.org/)。

### 实战：

1. 拉取镜像到本地：

   `service docker start                                   启动docker`

   `docker pull medicean/vulapps:t_thinkphp_2               拉取镜像到本地`

    `docker run -d -p 80:80 medicean/vulapps:t_thinkphp_2   启动环境` 

    如下图：

   ![image-20201115184054122](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201115184054122.png)

2. 启动环境：

   此时访问80端口：出现下图表明环境启动成功：

   ![image20201115194651623](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image20201115194651623.png)

3. 使用pocsuite验证与利用：

   `poc-console 			打开pocsuite交互模式`

   ![image-20201115185910037](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201115185910037.png)

   `search thinkphp       搜索适用与thinkphp的漏洞poc`

   ![image-20201115185923491](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201115185923491.png)

   `use  [options]      使用对应的poc`

   `showoptions       列出该poc所要设置的参数值`

   ![image-20201115190012474](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201115190012474.png)

   `set target  ip`

   `set lport  port  设置ip和端口` 

   `run            运行poc`  

   ![image-20201115195140207](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201115195140207.png)

### 总结：

个人认为使用docker搭建靶机测试环境实在是非常方便快捷的一种方式。可以让你省去许多和渗透工作无关的环境配置问题与麻烦。另外，pocsuite也是一款免费开源十分好用的漏洞检测工具，而且可以根据自己的需求定制自己的模块，更多功能等你发现。附上[poc源码](https://co0ontty.github.io/2019/08/12/thinkphp_5_rce.html)以及[Pocsuite官网地址](https://pocsuite.org/)，需要自取。