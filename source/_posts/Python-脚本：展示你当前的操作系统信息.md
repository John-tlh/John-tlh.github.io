---
title: Python 脚本：展示你当前的操作系统信息
category: 
- 编程开发
tags: 
- Python
---

## 脚本描述

- 展示操作系统信息

## 脚本source

```python
import platform as pl

profile = [
    'architecture',
    'linux_distribution',
    'mac_ver',
    'machine',
    'node',
    'platform',
    'processor',
    'python_build',
    'python_compiler',
    'python_version',
    'release',
    'system',
    'uname',
    'version',
]


class bcolors:
    HEADER = '\033[95m'
    OKBLUE = '\033[94m'
    OKGREEN = '\033[92m'
    WARNING = '\033[93m'
    FAIL = '\033[91m'
    ENDC = '\033[0m'
    BOLD = '\033[1m'
    UNDERLINE = '\033[4m'


for key in profile:
    if hasattr(pl, key):
        print(key + bcolors.BOLD + ": " + str(getattr(pl, key)()) + bcolors.ENDC)
```

## 脚本演示

![image-20201207210443623](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201207210443623.png)

可以试试在linux下运行此脚本看看效果：

![image-20201207210922229](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201207210922229.png)

以上输出的是我的kali虚拟机操作系统的信息。

<!-- more -->