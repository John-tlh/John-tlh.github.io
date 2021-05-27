---
title: sql注入学习2
category: 
- 渗透测试
tags: 
- web安全
---

sql注入的流程

## 目标搜集

- 无特定目标

  inurl:.xxx?xx=

- 有特定目标

  inurl:.xxx?xx=  site:xxxx.com

- 使用自动话工具爬取

![image-20201220173113674](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201220173113674.png)

### 注入识别

- 手工简单识别

  ` + '`

  `and 1=1 /and 1=2`

  `and '1'='1' /and '1'='2`

  `and 1 like 1 /and 1 like 2`

- 工具识别

  `sqlmap -m filename` (检测目标文件)

  `sqlmap  --crawl`  (对网站进行爬取然后依次进行测试)

- 高级识别

  扩展识别深度和广度

  `sqlmap --level`   识别其它参数

  `sqlmap  -r`  识别数据包
  
  利用工具提高识别效率 比如在burp中安装sqlmap扩展直接调用sqlmap进行测试
  
  所需环境：python2 burpsuite sqlmap jython 
  
  首先安装jython
  
  ![image-20201220181141327](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/20202020image-20201220181141327.png)
  
  然后配置jython：
  
  ![image-20201220181410767](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/20202020image-20201220181410767.png)
  
  然后安装扩展：
  
  ![image-20201220181613794](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/20202020image-20201220181613794.png)
  
  安装完成后启动服务即可：
  
  ![image-20201220221855762](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201220221855762.png)
  
  使用就自己取摸索了。
  
- 其它方面

  ![image-20201220195600458](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201220195600458.png)

- 代码审计（百盒测试）

简单说的话：流程是这个样子的

![image-20201220201225090](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201220201225090.png)

<!-- more -->