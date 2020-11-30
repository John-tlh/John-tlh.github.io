---
title: 图形化安装Kali虚拟机
category: 
- 渗透测试
tags: 
- Kali
- Tools
---

## 目的

- 在虚拟机中安装kali，作为学习安全知识的攻击机。

## 工具

- [VMwarePro 16](https://pan.baidu.com/s/1BAmzDWcPMRcF_WQorqRavQ)提取码:`qygn`
- [Kali2019.iso](https://pan.baidu.com/s/1hmFnUCnG3DHWJLDXjw7w4A))提取码:`uo46`

:artificial_satellite:点击链接即可下载

## 过程

安装过程中需要注意两个地方，其他地方默认即可：

![image-20201124205100830](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/20202020image-20201124205100830.png)

1. 导入镜像文件，打开虚拟机会进入到如下安装界面。切记选择图形化安装（对于新手特别注意）
2. 在进行磁盘分区时候，推荐新手也使用默认设置即可。最后选择将修改写入磁盘一项勾选。
3. 软件源的安装建议先跳过。

<!-- more -->

## 一些建议

1. 选择虚拟机磁盘空间大小时，建议可以选大一点。默认情况下是20g，然而kali里面预装了许多软件，基本上20个g很快就会用完。如果大家不希望到时候自己进行磁盘扩展和分区的化，建议一步到位，直接给到100g以上。
2. 建议开启共享文件夹，实现主机与虚拟机的数据传输。
3. 建议安装VMtools，简化虚拟机的ui以及操作。

