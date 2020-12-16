---
title: Python 脚本：创建一个目录
category: 
- 编程开发
tags: 
- Python


---

## 脚本描述

- 创建一个空目录

## 脚本source

```python
import os  # 导入OS模块

MESSAGE = 'The directory already exists.'
TESTDIR = 'testdir'
try:
    home = os.path.expanduser("~")  # 设置home目录位置
    print(home)  # 打印路径

    if not os.path.exists(os.path.join(home, TESTDIR)):  # os.path.join() 绝对路径
        os.makedirs(os.path.join(home, TESTDIR))  # 如果不存在这个目录就创建
    else:
        print(MESSAGE)
except Exception as e:
    print(e)
```

## 脚本演示

![image-20201207210106452](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201207210106452.png)

可以看到，在用户家目录有一个testdir目录（因为之前运行过所以提示目录已存在）

<!-- more -->