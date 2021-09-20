---
title: metasploit 学习01
category: 
- 渗透测试
tags: 
- metasploit
---

## metasploit 学习01

**简介：**

R语言编写的开源工具，模板化框架，有很好的扩展性。

**模块介绍：**

Auxiliaries(辅助模块):扫描、搜索漏洞

Exploit(漏洞利用模块):漏洞利用

Payload(攻击载荷模块):发送payload

Post(后渗透模块):后渗透

Encoders(编码工具模块):免杀、绕过

**攻击步骤：**

1. 扫描目标系统寻找漏洞
2. 配置一个exp模块
3. 配置payload
4. 选择编码
5. run

**实例1：**使用msf进行端口扫描（TCP探测）

```sh
//代码如下
msfconsole
search portscan
use auciliar/scanner/portscan/tcp
set rhosts xxx.xxx.xxx.xxx
set ports 1-10000
set threads 20
show options
run
```

截图如下：

![image-20210613010129424](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/image-20210613010129424.png)

结果如下：

![image-20210613010142629](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/image-20210613010142629.png)

**实例2：**使用msf调用nmap进行服务探测、扫描

![image-20210613010154859](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/image-20210613010154859.png)

<!-- more -->