---
title: Kali linux下通过Clash访问外网
category: 
- 渗透测试
tags: 
- Kali
---

## 目的

渗透测试需要接触到许多工具，很多都需要你有一个畅通的网络环境。因此，学会在kali下使用代理对于渗透工作者来说是非常重要的。

## 前期准备

1. 了解clash，登录clash仪表盘
2. 下载 https://github.com/Dreamacro/clash 的发行版本（）本例中使用的是`clash-linux-amd64-v1.3.0.gz`
3. 在/root 下新建文件夹 clash
4. 将下载来的.gz文件解压到clash（为了方便启动我把解压后的文件重命名未来clash）目录结构如下

```
/root
-----/clash
-----------clash(解压得到的可执行文件）
```

至此，准备工作都已完成。

## 开始安装

- ### 步骤1

直接运行当前目录下的可执行文件,然后查看`/root/.config/clash`下是否生成了两个新文件：

```
config.yml
Country.mmdb
```

如果有，说明准备工作做得没错。

<!-- more -->

- ### 步骤2---替换掉这两个文件：

替换config.yml(先将旧的删掉然后运行以下代码会生成新的)

```bash
curl -H "User-Agent: ClashX/1.20.4.1" https://glados-remote.com/clash/49644/8e2488c/21889/glados_new.yaml > config.yaml
```

[替换](https://pan.baidu.com/s/1oEbscsfIB9pKVrCvwYauvw )掉`Country.mmdb` 提取码：`rwje`

替换完后，将这连个文件再复制到你自己的运行目录下。也就是/root/clash/下

做完后目录结构如下：

![image-20201201174737236](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201201174737236.png)

![image-20201201174754989](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201201174754989.png)

接下来  设置系统代理如下：

![image-20201201174841445](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201201174841445.png)

浏览器代理如下：

![image-20201201174956608](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201201174956608.png)

最后 检查代理是否成功：

![image-20201201175037571](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201201175037571.png)

教程所有[资源](https://pan.baidu.com/s/1OF1OvuxOp1gi9XDo3P5YJA)打包如下，放在百度网盘。提取码：`clas`

## 注意事项

目录结构有点绕，具体怎么样想搞懂自己去看一下官网文档。

如果没有接触过clash 建议先在Windows下代理成功，再去学怎么给虚拟机上代理。