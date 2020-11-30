---
title: kali 下安装CyberMap 自动化渗透测试工具
category: 
- 渗透测试
tags: 
- Kali
---

## 工具介绍

- {1} Scanning open ports
- {2} OS detection
- {3} Scan your network
- {4} Scan the most popular ports
- {5} Scan TCP or UDP protocols
- {6} Standard service detection
- {7} Detect Firewall Settings
- {8} Identify hostnames
- {9} Scan a firewall for MAC address spoofing
- {10} Scan a single port
- {11} Default script scan
- {12} Detect heartbleed SSL vulnerability
- {13} IP address information
- {14} Scan filtered ports
- {15} Scan list of hosts from a file
- {16} Scan an IP address range
- {17} Aggressive and obtrusive scan
- {18} XML output

![cyber](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020cyber.gif)

## 安装方法

```bash
git clone https://github.com/AnonymousAt3/cybermap.git
```

```bash
cd cybermap
chmod +x cybermap.sh
./cybermap.sh
```

note: run in root account.

![image-20201130202056355](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201130202056355.png)

安装后运行，界面如下：

![image-20201130202216071](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201130202216071.png)

## 演示使用

<!-- more -->

- 扫描开放端口

![image-20201130204232553](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201130204232553.png)

- 操作系统探测

- 扫描网段
- 扫描TCP/UDP协议
- 扫描最常用的端口
- 主机服务探测
- 探测防火墙
- 主机识别
- MAC地址探测
- 扫描单个端口
- 脚本扫描
- 探测严重的ssl 漏洞
- ip whois信息
- 扫描过滤掉的端口
- 从文件中批量扫描主机
- 扫描ip地址段
- XML输出

具体使用这里不一一列出，大家有兴趣自己动手实践一下。

