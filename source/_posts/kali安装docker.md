---
title: kali安装docker
category: 
- 渗透测试
tags: 
- Kali
- Tools
- Docker
---

# kali安装docker

使用kali安装docker非常简单。只需几条命令。

- ### 先添加更新源

```bash
deb http://mirrors.zju.edu.cn/kali kali-rolling main contrib non-free

deb-src http://mirrors.zju.edu.cn/kali kali-rolling main contrib non-free
```

- ### 执行以下命令

```
curl -fsSL http://mirrors.zju.edu.cn/docker-ce/linux/debian/gpg | sudo apt-key add - 

echo 'deb http://mirrors.zju.edu.cn/docker-ce/linux/debian/ buster stable' | sudo tee /etc/apt/sources.list.d/docker.list 

apt-get update

apt-get install docker-ce
```

注意：安装过程中需要手动输入确认信息。请注意安装进度。

- ### 启动docker

```
systemctl start docker
docker --version
```

出现如下界面即为安装成功：

![image-20201125221956553](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201125221956553.png)

<!-- more -->