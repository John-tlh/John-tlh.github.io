---
title: Kali 安装后必做的10件事
category: 
- 渗透测试
tags: 
- Kali
- Tools
---

## 换软件源

首先先查看kali 中源的文件，里面默认有官方的源。

```bash
vim /etc/apt/sources.list
```

将官方的源进行注释。

![image-20201125164936415](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201125164936415.png)

然后把我们找到的国内的源添加上

![image-20201125165115203](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201125165115203.png)

:artificial_satellite:附上国内比较常用的源清单：

<!-- more -->

```
#阿里云kali源 
deb http://mirrors.aliyun.com/kali kali main non-free contrib 
deb-src http://mirrors.aliyun.com/kali kali main non-free contrib 
deb http://mirrors.aliyun.com/kali-security kali/updates main contrib non-free
#163 Kali源 
deb http://mirrors.163.com/debian wheezy main non-free contrib 
deb-src http://mirrors.163.com/debian wheezy main non-free contrib 
deb http://mirrors.163.com/debian wheezy-proposed-updates main non-free contrib 
deb-src http://mirrors.163.com/debian wheezy-proposed-updates main non-free contrib 
deb-src http://mirrors.163.com/debian-security wheezy/updates main non-free contrib 
deb http://mirrors.163.com/debian-security wheezy/updates main non-free contrib 
#中科大 
deb http://mirrors.ustc.edu.cn/kali kali-rolling main non-free contrib 
deb-src http://mirrors.ustc.edu.cn/kali kali-rolling main non-free contrib
#浙大 
deb http://mirrors.zju.edu.cn/kali kali-rolling main contrib non-free 
deb-src http://mirrors.zju.edu.cn/kali kali-rolling main contrib non-free
#清华大学 
deb http://mirrors.tuna.tsinghua.edu.cn/kali kali-rolling main contrib non-free 
deb-src https://mirrors.tuna.tsinghua.edu.cn/kali kali-rolling main contrib non-free 
```

确认无误即可。推荐中科大，个人觉得很不错。

更新完毕后会弹出几个图形界面需要你确认选项，默认情况下接受默认选项即可。

:artificial_satellite:事实上这只是对于国内用户而言必须的操作。其实我更偏向于说从根本上解决这个问题---直接绕过GWF访问外网。

## 更新软件、升级系统

```bash
$ sudo apt-get clean 
$ sudo apt-get update 
$ sudo apt-get upgrade -y 
$ sudo apt-get dist-upgrade -y
```

所有这些做完后应该会出现如下界面：

![image-20201125181341938](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201125181341938.png)

## 自定义kali Linux 的外观

```bash
$ sudo apt install gnome-tweaks
$ gnome-tweaks
```

![image-20201125171558061](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201125171558061.png)

## 安装Filezilla 客户端（可选项）

```bash
$ sudo apt install filezilla filezilla-common -y
$ sudo filezilla
```

![image-20201125182415600](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201125182415600.png)

:artificial_satellite:关于Filezilla的用途这里不叙述，有这个需求的可以看看[这篇文章]()。

## 安装Tor Browser

```bash
$ sudo apt install tor
```

:artificial_satellite:挂代理，匿名访问。不要搞别人最好也别被别人搞。

## 禁用屏幕锁定（看自己喜好）

![image-20201125205602688](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201125205602688.png)

## 安装应用商店

```bash
$ sudo apt install software-center
```

:artificial_satellite:上面的tor和应用商店安装都只适用于已经可以直连外网的kali linux

## 安装Git

```bash
$ sudo apt-get install git
```

## 安装一款编辑器

推荐使用Atom

## 最重要的千万别忘了！

我觉得第一件事应该是找一个好看的墙纸hhhh~