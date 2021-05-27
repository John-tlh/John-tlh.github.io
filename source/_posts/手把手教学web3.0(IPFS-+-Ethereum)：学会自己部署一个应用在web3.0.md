---
title: 手把手教学web3.0(IPFS + Ethereum)：学会自己部署一个应用在web3.0
category: 
- 随笔
tags: 
- web3.0
---

## 翻译：[Learn Web 3.0 by actually Deploying an Application on it: Hands-On Approach (IPFS + Ethereum)](https://hackernoon.com/learn-web-3-0-by-actually-deploying-an-application-on-it-hands-on-approach-9141ad88588f)

### 简介

去中心化web或者说web3.0已经成了如今的流行语，因为他们给当今的互联网业带来了革命性质的巨变。但有多少人真的了解web3.0呢？这篇文章涵盖了web3.0的几个主要特性。在掌握了这些基本知识之后，我将带大家在[IPFS](https://hackernoon.com/tagged/ipfs)上部署一个web3.0的应用。该应用程序具有在[以太坊](https://hackernoon.com/tagged/ethereum)虚拟机上运行的可靠的智能合约。通过使用以太坊+IPFS的组合，真正使得这个应用成为了一个去中心化的应用。

![1_tU-ezv8Ub7MWr19MDAn8pw](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/20201_tU-ezv8Ub7MWr19MDAn8pw.gif)

让我们开始吧！

### 正文

#### 为什么web3.0对我们来说很重要？

因特网诞生之初我们叫他为web1.0，这时候的web大都是静态的。没有任何交互功能。这时候的人们访问互联网是完全匿名且隐私信息是完全安全的，因为这时候的互联网上还不曾发展出交易买卖等等功能。此时的web像地狱一样寂静。我们今天根本难以想象当时的情形。然后我们在20世纪90年代迎来了web2.0。web2.0的到来催生了一批巨人企业像Alphabet, Amazon, Microsoft等等。这时期，网络上出现了大量的交互活动但同时个人隐私沦为了别人的’玩物‘。

![image-20210220155230836](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20210220155230836.png)

web3.0使参与网络的用户完全掌控他们自己的个人数据，努力想用这种方式帮助用户重新’拿回‘他们的隐私。web3.0是有民主保障的而非被少数巨头垄断，是去中心化而非中心化的网络。从web2.0转向web3.0的过程将是逐步的，而非一夜之间。但是加快这种转变最快的方式就是将这种意识传递到更多人之中。 当用户需求发生变化时，当前的业务需求也会发生变化。用户需要意识到自己才是自己个人数据的主人！如果有任何人通过你的个人数据赚到了钱，那么这个钱理应是你的。

![image-20210220160142064](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20210220160142064.png)

![1_Bx7CQB9UWpJgctkjFTlhyQ](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/20201_Bx7CQB9UWpJgctkjFTlhyQ.png)

![1_dottislVqks8AWsVrdbl8A](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/20201_dottislVqks8AWsVrdbl8A.png)

#### web3.0的一些特性

- 没有中央控制点：像Google，Microsoft，Amazon这样的公司将不再拥有对您数据的控制权。没有政府机构能够阻止网站和限制服务。像以太坊这样的区块链将会大放异彩，简而言之，中间人这种模式将完全不合时宜。
- 数据所有权：最终用户将重新获得对数据的完全控制，并具有加密的安全性。目前，诸如亚马逊和Facebook之类的大公司拥有庞大的数据仓库，用于存储价值数十亿美元的用户数据以改善其服务。
- 大大减少黑客攻击和数据泄露：因为数据将是去中心化的和分发的，所以黑客将很难找到系统的单个入口。
- 互通性：应用程序将易于定制且与设备无关，能够在智能手机，电视，汽车，微波炉和智能传感器上运行。当前，应用程序是特定于OS的，并且通常限于单个操作系统。例如，许多Android加密货币钱包在iO上不可用，这使使用多种设备的消费者感到不便。对于负责发布多次迭代和软件更新的开发人员，这会增加额外花费与精力。
- 无许可的区块链：财富和其他数字资产可以在世界任何地方快速，高效地跨境转移。
- 不间断服务：帐户吊销和分布式拒绝服务大大减少了。由于没有单点故障，因此服务中断将降至最低。数据将存储在分布式节点上，以确保冗余，并且多个备份将防止服务器故障或卡死。

Check out the awesome [Internet of Blockchain Foundation](https://iobf.co/) for more!

### 实操--time for hands-on learing。

为了节省时间和篇幅，我已经准备了基本代码。首先，git从我的Github页面[克隆](https://github.com/niharrs/Blockchain-Voting)存储库。

这是一个基本的民意调查应用程序，它在“朋友”和“我如何与您的母亲见面”这两档节目之间进行民意测验。 （这两个是美国非常著名的电视节目。）我个人很喜欢Friends！

要顺利运行该应用程序，请确保已安装以下组件：

- NodeJS
- Truffle Framework
- Ganacha
- Metamask Chrome Extension

确保Ganacha一直在运行。要运行该应用程序，请打开控制台并输入以下命令：

<!-- more -->