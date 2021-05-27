---
title: 当你拥有一台高性能vps(cpu挖矿：门罗币)
category: 
- 编程
tags: 
- 挖矿
---

## 当你拥有一台高性能vps

### 前言

最近入手一台vultr高性能服务器，具体配置如图：

![image-20210215003049893](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20210215003049893.png)

这个配置对应的花费大概是：80$/months。附上我目前的余额：

![image-20210215003204273](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20210215003204273.png)

那么我是远远用不了这么高的配置的，所以我想了想对于我来说有几个方案：

1. 模拟一下企业的内网环境，搭建一个企业内网环境用来渗透学习（懒、还未开始）
2. 做一个扫描器，调用masscan+nmap做一个快速、准确、大范围的web扫描器（已经实现，具体效果有时间也会写篇文章分享一下，可以快速扫描一个子域或者一个c段甚至b段）
3. 搭建n多漏洞环境作为公共靶场进行学习（这个想想算了，没啥意义）
4. 听说门罗币（cpu）挖矿挺火，可以试着搞一下

下面给出使用这台vps挖掘门罗币的详细步骤以及最终的实际效果，想直接查看结果的朋友可以直接跳过步骤部分。

### 步骤

- 申请一个门罗钱包

这一步没什么好说的，直接点进门罗钱包官网申请一个[钱包地址](https://wallet.mymonero.com/)就行（注意保存好自己的密钥）

- 选择一个矿池

其实google一下门罗矿池会有很多好的平台以及挖矿工具供大家选择，我这里使用的是[Nanopool]()这个矿池，进去之后无需注册，点击help，点击step by step。 然后直接阅读教程即可。（肯定比我讲的详细、严谨）

![image-20210215004421377](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20210215004421377.png)

- 下载挖矿软件

如果大家使用的是我上面推荐的平台，那么他那个教程已经把它对应的工具给出来了。大家仔细阅读完教程后，下载好平台提供的挖矿软件，然后就可以开心的挖矿了。注意下载对应自己的版本，比如我的os是ubuntu。所以我会下载linux下的。你觉得自己的pc机很强大的话你也可以玩一玩:v:

工具下载界面长这样：

![image-20210215005346720](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20210215005346720.png)

- 开始挖矿

ubuntu下非常简单：直接下载然后解压即可：

```
wget https://github.com/nanopool/nanominer/releases/download/v3.2.2/nanominer-linux-3.2.2.tar.gz
tar -zxvf filename. tar.gz
```

接着进到解压目录，vim一下config.ini文件。按照平台的说明写上自己的钱包地址、邮箱啥的。然后执行：./nanomaner

![image-20210215010151589](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20210215010151589.png)

这个工具运行时会告诉你他当前接收到的新任务以及shares数量：如下图

![image-20210215010336289](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20210215010336289.png)

你可以开另一个shell去监控你的系统cpu使用率：可以使用top命令：如图所示：

![image-20210215010456120](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20210215010456120.png)

可以看到这里的cpu占用率 已经是极限了:v:

看一下vps后台：em确实是极限了。

![image-20210215010619255](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20210215010619255.png)

如果大家想看现在挖到了多少矿，可以登入之前那个平台官网，右上角输入你的钱包地址，然后就可以看到啦。给大家看一下我的：

![image-20210215011055961](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20210215011055961.png)

### 实际效果

好了。其实实际结果怎么样大家已经心中有数了。我当前半个小时挖矿的收益如上。我想想哈，按照这个速率，我一个月躺着挣钱的收入大概是：0.4$

em，就是这样。所以 我觉得我这篇文章是非常有教育意义的，是哪种教育意义我就不明说了，没时间了，我先去把我的vps关了先:call_me_hand:

ps:sagittarius:我之所以说躺着赚钱得收益，是因为这台vps并非我自己购买所得，账户余额里面那一百多刀我实际上只充值了10$.

大家如果也想使用这个充10$送100$的vps平台，可以[在这儿去申请](https://www.vultr.com/?ref=8796241)这个优惠(优惠时间有限，大家注意看清楚哦！)

<!-- more -->

