---
title: Python 脚本：自动生成指定网段IP
category: 
- 编程开发
tags: 
- Python
---

## 脚本描述

- 可以批量生成或者定制你想要的ip地址段

## 脚本source

```python
#!/usr/bin/env python
# -*- coding:utf-8 -*-

import time

time_start = time.time()    #设置运行开始时间

# 批量生成IP地址 并且写入文件中
def get_ip(numbel, start):
    file = open('gip.txt', 'w')
    starts = start.split('.')
    A = int(starts[0])
    B = int(starts[1])
    C = int(starts[2])
    D = int(starts[3])
# 这里A B C D 的值为 192 168 23 0
# 接下来 生成网络号为192.168.23.0/24 所有0-255个主机位（广播位）
    for D in range(D, 256):
        ip = "%d.%d.%d.%d" % (A, B, C, D) #将ABCD的值赋予ip
        if numbel > 1:
            file.write(ip + '\n')
            numbel -= 1
        elif numbel == 1: #解决最后一行回车问题
            file.write(ip)
            numbel -= 1
        else:
            file.close()
            print(ip)
            return

#   将生成的文件保存为字典格式并且通过dict[i]来获取该ip地址输出到控制台
def readIp():
    ipfile = 'gip.txt'
    global iplist
    iplist = {}

    with open(ipfile, 'r') as file_to_read:
        for i in range(0, 256):
            lines = file_to_read.readline() #整行读取数据
            if not lines:
                break
            ip = lines.replace('\n', '') #自动换行
            iplist[i] = ip
            print(iplist[i])

#  程序入口
if __name__ == '__main__':
    get_ip(255, '192.168.23.0')
    time_end = time.time()
    time = time_end - time_start
    print('耗时%s秒' % time)

    #读取文件内容输出到控制台
    readIp()
    print('读取结束')
```

## 脚本演示

![pyshell](C:\Users\krill\Desktop\pyshell.gif)

<!-- more -->

