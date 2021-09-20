---
title: python爬虫学习day1
category: 
- 编程
tags: 
- python'
---

记录了一下python3爬虫实现用到的一些模块，主要用了urllib包中的request、response、parse 模块。为了以后方便查找，记录一下：

**urllib的使用**

```python
# !/usr/bin/env python
# encoding: utf-8
'''
  @author: kriller
  @license: (C) Copyright 2013-2017, Node Supply Chain Manager Corporation Limited.
  @contact: kriller@cumt.edu.cn
  @file: urllib_test.py
  @time: 2021/6/15 11:55
  @desc: urllib主要用到urllib.request 以及urllib.parse 其中urllib.request 中主要用到urlopen以及urlretrieve两个方法
  下面是实例演示
  '''
import urllib.request as rq
import urllib.parse as parse

# url = 'http://www.baidu.com'
#
# response = rq.urlopen(url)

# print(response.read().decode('utf-8'))
# urlopen 返回的是一个对象,该对象有 read()、geturl()、getheaders()、getcode()、readlines() 方法
# read 方法返回的是字节对象，如果需要返回文本，需要进行decode('对应网页编码')
# print(response.geturl())
# print(response.getcode())
# print(response.getheaders())
# print(response.readlines())

# 将返回的网页文本写入文件中
# with open('baidu.html','w', encoding='utf-8') as fp:
#     fp.write(response.read().decode())

# 下载一张图片：
# 方法1图片只能写入本地二进制
#imgurl = 'https://raw.githubusercontent.com/John-tlh/blog/master/imagesdff0648ea3163cbe403c144932470520.jpg'
#
# res1 = rq.urlopen(imgurl)
#
# with open('bd.jpg','wb') as im:
#     im.write(res1.read())

# 方法2 使用request.urlretrieve

# rq.urlretrieve(imgurl,'bd_back.jpg')

#urlparse
# 测试urlparde中的quote方法 编解码
# imaurl = 'https://www.baidu.com/link?url=fmp_Fb1llQ_tDkQUMFvC4nfd_KY9rJGhOQIz6erl9Fr8xkcykyKAadZ0TAVeVjRK_JKpv6-Wlg67nV7xttk65_O_g2ER--llKAeETSsS3pPNfrC9M4yfjtHfnO75cFjlHgcU3poGlbfSx5OSx3CJx7uH9zD1yiGxoviIZSgb8lQEiQP8D31MsYyk0SYyjZEFXoYtd5pXOIcUv-BE2Xv8ybbhbSyCLYU3PcukOvdj7e_eTY9RsrnW3y4NEs9rb7HcF2OEOHjpROXSOmwSGwP88xchUAdTLYVll7gibpdf7nwfdnZdVSvP1Ak9li0rUU-ywaZ5qPGLNk8dfH6sNXnJ40SFhwS2DP3p0JZ8rUHJ5qRAPXYndXzCitnf5IJ8TFq2OLPj3XM8Ik_IodFiSSTPJFmepNQVhbl4BCQoRfKmawrnidPclM5R3fOw0gOxyjGY4Ir_h0rGA5MVql8-KNKNVd-YWBpMMReXUIIuntoe-lK&click_t=1623735162241&s_info=1003_990&wd=&eqid=a71ff3180015b1860000000260c83b75'
#
# print(parse.quote(imaurl))

# 拼接多个get 参数到url中
#方法一:自己写
data = {
    'name': 'xxh',
    'age': 18,
    'sex': '男',
    'height': 20,
}

# 遍历字典
# lt = []
# for k, v in data.items():
#     lt.append(k+ '=' + str(v))
# #print(lt) ['name=xxh', 'age=18', 'sex=男', 'height=20']
# query_string = '&'.join(lt)
# #print(query_string) name=xxh&age=18&sex=男&height=20


#方法2: parse.urlencode(data)
query_str = parse.urlencode(data)
print(query_str)
url = 'http://www.baidu.com'+'?'+query_str
print(url)

#更推荐用urldecode(),会对中文进行转义
```

**自定义请求头(随机UA) 发起get请求**

```python
# !/usr/bin/env python
# encoding: utf-8
'''
  @author: kriller
  @license: (C) Copyright 2013-2017, Node Supply Chain Manager Corporation Limited.
  @contact: kriller@cumt.edu.cn
  @file: get_test.py
  @time: 2021/6/15 16:27
  @desc: 自定义请求头(随机UA) 发起get请求
  '''
import urllib.request as request
import urllib.parse as parse
import random


def getheaders():
    # 随机ua池
    user_agent_list = [
      'Mozilla/5.0 (Windows NT 10.0; Win64; ''x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36',
      'Mozilla/5.0 (Windows NT 6.2; WOW64) AppleWebKit/537.36 (KHTML like Gecko) Chrome/44.0.2403.155 Safari/537.36',
      'Mozilla/5.0 (Macintosh; U; PPC Mac OS X; pl-PL; rv:1.0.1) Gecko/20021111 Chimera/0.6',
      'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/41.0.2227.1 Safari/537.36',
      'Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/41.0.2227.0 Safari/537.36',
      'Mozilla/5.0 (Macintosh; U; PPC Mac OS X; en) AppleWebKit/418.8 (KHTML, like Gecko, Safari) Cheshire/1.0.UNOFFICIAL',
      'Mozilla/5.0 (X11; U; Linux i686; nl; rv:1.8.1b2) Gecko/20060821 BonEcho/2.0b2 (Debian-1.99+2.0b2+dfsg-1)',
      'Mozilla/5.0 (Macintosh; U; Intel Mac OS X 10_6_8; en-us) AppleWebKit/534.50 (KHTML, like Gecko) Version/5.1 Safari/534.50',
      'Mozilla/5.0 (Windows; U; Windows NT 6.1; en-us) AppleWebKit/534.50 (KHTML, like Gecko) Version/5.1 Safari/534.50',
      'Mozilla/5.0 (compatible; MSIE 9.0; Windows NT 6.1; Trident/5.0',
      'Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 6.0; Trident/4.0)',
      'Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 6.0)',
      'Mozilla/5.0 (Windows NT 6.1; rv:2.0.1) Gecko/20100101 Firefox/4.0.1',
      'Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/45.0.2454.101 Safari/537.36',
      'Opera/9.80 (Macintosh; Intel Mac OS X 10.6.8; U; en) Presto/2.8.131 Version/11.11',
      'Opera/9.80 (Windows NT 6.1; U; en) Presto/2.8.131 Version/11.11',
      'Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1; The World)',
      'Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/30.0.1599.101 Safari/537.36',
      'Mozilla/5.0 (Windows NT 6.1; WOW64; Trident/7.0; rv:11.0) like Gecko',
      'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/80.0.3987.132 Safari/537.36',
      "Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; AcooBrowser; .NET CLR 1.1.4322; .NET CLR 2.0.50727)",
      "Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 6.0; Acoo Browser; SLCC1; .NET CLR 2.0.50727; Media Center PC 5.0; .NET CLR 3.0.04506)",
      "Mozilla/4.0 (compatible; MSIE 7.0; AOL 9.5; AOLBuild 4337.35; Windows NT 5.1; .NET CLR 1.1.4322; .NET CLR 2.0.50727)",
      "Mozilla/5.0 (Windows; U; MSIE 9.0; Windows NT 9.0; en-US)",
      "Mozilla/5.0 (compatible; MSIE 9.0; Windows NT 6.1; Win64; x64; Trident/5.0; .NET CLR 3.5.30729; .NET CLR 3.0.30729; .NET CLR 2.0.50727; Media Center PC 6.0)",
      "Mozilla/5.0 (compatible; MSIE 8.0; Windows NT 6.0; Trident/4.0; WOW64; Trident/4.0; SLCC2; .NET CLR 2.0.50727; .NET CLR 3.5.30729; .NET CLR 3.0.30729; .NET CLR 1.0.3705; .NET CLR 1.1.4322)",
      "Mozilla/4.0 (compatible; MSIE 7.0b; Windows NT 5.2; .NET CLR 1.1.4322; .NET CLR 2.0.50727; InfoPath.2; .NET CLR 3.0.04506.30)",
      "Mozilla/5.0 (Windows; U; Windows NT 5.1; zh-CN) AppleWebKit/523.15 (KHTML, like Gecko, Safari/419.3) Arora/0.3 (Change: 287 c9dfb30)",
      "Mozilla/5.0 (X11; U; Linux; en-US) AppleWebKit/527+ (KHTML, like Gecko, Safari/419.3) Arora/0.6",
      "Mozilla/5.0 (Windows; U; Windows NT 5.1; en-US; rv:1.8.1.2pre) Gecko/20070215 K-Ninja/2.1.1",
      "Mozilla/5.0 (Windows; U; Windows NT 5.1; zh-CN; rv:1.9) Gecko/20080705 Firefox/3.0 Kapiko/3.0",
      "Mozilla/5.0 (X11; Linux i686; U;) Gecko/20070322 Kazehakase/0.4.5",
      "Mozilla/5.0 (X11; U; Linux i686; en-US; rv:1.9.0.8) Gecko Fedora/1.9.0.8-1.fc10 Kazehakase/0.5.6",
      "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/535.11 (KHTML, like Gecko) Chrome/17.0.963.56 Safari/535.11",
      "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_7_3) AppleWebKit/535.20 (KHTML, like Gecko) Chrome/19.0.1036.7 Safari/535.20",
      "Opera/9.80 (Macintosh; Intel Mac OS X 10.6.8; U; fr) Presto/2.9.168 Version/11.52",
      "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/536.11 (KHTML, like Gecko) Chrome/20.0.1132.11 TaoBrowser/2.0 Safari/536.11",
      "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.1 (KHTML, like Gecko) Chrome/21.0.1180.71 Safari/537.1 LBBROWSER",
      "Mozilla/5.0 (compatible; MSIE 9.0; Windows NT 6.1; WOW64; Trident/5.0; SLCC2; .NET CLR 2.0.50727; .NET CLR 3.5.30729; .NET CLR 3.0.30729; Media Center PC 6.0; .NET4.0C; .NET4.0E; LBBROWSER)",
      "Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; QQDownload 732; .NET4.0C; .NET4.0E; LBBROWSER)",
      "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/535.11 (KHTML, like Gecko) Chrome/17.0.963.84 Safari/535.11 LBBROWSER",
      "Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 6.1; WOW64; Trident/5.0; SLCC2; .NET CLR 2.0.50727; .NET CLR 3.5.30729; .NET CLR 3.0.30729; Media Center PC 6.0; .NET4.0C; .NET4.0E)",
      "Mozilla/5.0 (compatible; MSIE 9.0; Windows NT 6.1; WOW64; Trident/5.0; SLCC2; .NET CLR 2.0.50727; .NET CLR 3.5.30729; .NET CLR 3.0.30729; Media Center PC 6.0; .NET4.0C; .NET4.0E; QQBrowser/7.0.3698.400)",
      "Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; QQDownload 732; .NET4.0C; .NET4.0E)",
      "Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1; Trident/4.0; SV1; QQDownload 732; .NET4.0C; .NET4.0E; 360SE)",
      "Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; QQDownload 732; .NET4.0C; .NET4.0E)",
      "Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 6.1; WOW64; Trident/5.0; SLCC2; .NET CLR 2.0.50727; .NET CLR 3.5.30729; .NET CLR 3.0.30729; Media Center PC 6.0; .NET4.0C; .NET4.0E)",
      "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.1 (KHTML, like Gecko) Chrome/21.0.1180.89 Safari/537.1",
      "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.1 (KHTML, like Gecko) Chrome/21.0.1180.89 Safari/537.1",
      "Mozilla/5.0 (iPad; U; CPU OS 4_2_1 like Mac OS X; zh-cn) AppleWebKit/533.17.9 (KHTML, like Gecko) Version/5.0.2 Mobile/8C148 Safari/6533.18.5",
      "Mozilla/5.0 (Windows NT 6.1; Win64; x64; rv:2.0b13pre) Gecko/20110307 Firefox/4.0b13pre",
      "Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:16.0) Gecko/20100101 Firefox/16.0","Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.11 (KHTML, like Gecko) Chrome/23.0.1271.64 Safari/537.11",
      "Mozilla/5.0 (X11; U; Linux x86_64; zh-CN; rv:1.9.2.10) Gecko/20100922 Ubuntu/10.10 (maverick) Firefox/3.6.10",
      'Mozilla/5.0 (Windows NT 6.2) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/28.0.1464.0 Safari/537.36',
      'Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/31.0.1650.16 Safari/537.36',
      'Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/35.0.3319.102 Safari/537.36',
      'Mozilla/5.0 (X11; CrOS i686 3912.101.0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/27.0.1453.116 Safari/537.36',
      'Mozilla/5.0 (Windows NT 6.2; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/27.0.1453.93 Safari/537.36',
      'Mozilla/5.0 (Windows NT 6.2; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/32.0.1667.0 Safari/537.36',
      'Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:17.0) Gecko/20100101 Firefox/17.0.6',
      'Mozilla/5.0 (Windows NT 6.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/28.0.1468.0 Safari/537.36',
      'Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/41.0.2224.3 Safari/537.36',
      'Mozilla/5.0 (X11; CrOS i686 3912.101.0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/27.0.1453.116 Safari/537.36'
    ]

    uaa = random.choice(user_agent_list)
    print(type(uaa))
    header = {'User-Agent':uaa}
    print(header)

    return header

def  run():
  keyword = input("输入搜索内容")
  url = 'http://www.baidu.com/s?'
  # 参数写成一个字典
  data = {
    'ie': 'utf-8',
    'wd': keyword,
  }
  print(type(data))
  query_str = parse.urlencode(data);

  url += query_str
  # print(url)
  # 发送请求
  #构建请求对象
  request_ob = request.Request(url=url,headers=getheaders())
  #发送请求
  resp = request.urlopen(request_ob)
  filename = keyword + '.html'
  with open(filename, 'w', encoding='utf-8') as fp:
    fp.write(resp.read().decode())


if __name__ == '__main__':
    getheaders()
    run()
```

最后抓包,发现随机ua已经生效。

![image-20210615175738818](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/image-20210615175738818.png)

继续ing。