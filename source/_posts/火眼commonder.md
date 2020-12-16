---
title: 安装火眼旗下windows渗透机
category: 
- 渗透测试
---

## 目的

一个合适的渗透机对于渗透测试的重要性不言而喻。使用最多的应该是kali，依托于linux内核debean发行版。但是有时候，我们还是希望在某些场景下能够使用Windows平台下的工具。因此有一台windows操作系统的渗透机也是十分有必要的。

## [关于Commando](https://www.freebuf.com/sectool/200524.html)

火眼旗下麦迪安网络安全公司顾问以及Commando VM套件的联合创建者 Jake Barteaux 表示：

```
在进行内部渗透测试时，我身边的大部分渗透测试工程师都会先自行配置一个Windows测试环境。能不能把这个环境配置好，配得有多快，已然成为了衡量渗透测试工程师手艺高低的标准了。其中很多人都会再自己配置的环境中集成Commando中也有的工具，不过在对Windows进行渗透测试时大家并没有形成一个标准的工具集。
```

火眼本次推出的Commando VM套件面向Windows平台构建，属于此前发布的[FLARE VM](https://www.fireeye.com/blog/threat-research/2018/11/flare-vm-update.html)套件的全新迭代版本，后者专攻逆向工程和恶意软件分析，Commando VM功能更加全面，是Windows环境中内部渗透测试的首选平台。

使用基于Windows平台构建的虚拟机环境有以下几点明显优势：

1. 原生支持Windows和Active Directory；
2. 可作为C2框架的临时工作区；
3. 更便捷的共享和交互式操作支持；
4. 支持PowerView和BloodHound等工具；
5. 对测试目标不产生任何影响。

## 前期准备

- 需要准备一个win10 1803，1809，1903，1909， 或者2004的镜像
- 分配空间不低于60G硬盘空间
- 不低于2G 内存

[可以看下官方推荐的安装配置：](https://github.com/fireeye/commando-vm)

- Windows 10 2004
- 80+ GB Hard Drive
- 4+ GB RAM
- 2 network adapters

本次安装使用[win10 2004.iso镜像]()，需要自取。

```
/root
-----/clash
-----------clash(解压得到的可执行文件）
```

至此，准备工作都已完成。

## 开始安装

- 使用你的镜像创建并且配置虚拟机

> 确保虚拟机系统完全更新，这非常重要。一定要先将系统更新到最新版不然极有可能安装安装失败。

- 制作一个备份，以免到时候出错恢复不了。
- [下载安装脚本](https://github.com/fireeye/commando-vm)install.ps1
- 以管理员权限打开powershell
- 进到脚本文件所在目录，解锁安装脚本`Unblock-File .\install.ps1`
- 设置powershell运行权限位不受限制 `Set-ExecutionPolicy Unrestricted -f`
- 最后，执行脚本文件`.\install.ps1`

安装大概会进行3个小时。由于许多软件是国外的源，所以有条件的还是再开始运行安装脚本之前先挂上代理，我用的是clash，非常好用。如果不挂代理的话 我觉得装不装得起应该就随缘了，说不好 装三天都装不好。。。。。

下面贴一张安装过程中的截图：

![image-20201202173236703](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201202173236703.png)

## 安装完成

<!-- more -->

安装完成后的截图如下，感觉还是帅的有木有~~

![image-20201202183309149](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201202183309149.png)

## 检验效果

打开tools 文件夹，里面的目录结构是 是这个样子的：

![image-20201205205902474](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201205205902474.png)

下面使用nmap 命令行的形式扫描一个网段 看看效果：

![image-20201205221436384](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201205221436384.png)

最后和kali下使用nmap扫描对比了一下 其实扫描到的好像要比kali下扫描到的信息更多一些（也可能是时间、环境问题）这里就不讨论了。总之如果你希望整一个Windows操作系统的渗透机，这个还是值得推荐的。

有安装上的问题 或者资源问题都可以留言问我  也可以私信我。