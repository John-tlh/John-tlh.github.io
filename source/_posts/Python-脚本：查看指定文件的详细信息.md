---
title: Python 脚本：查看指定文件的详细信息
category: 
- 编程开发
tags: 
- Python

---

## 脚本描述

- 列出指定文件/目录的详细信息

## 脚本source

```python

from __future__ import print_function

import os
import stat  # 索引
import sys
import time

if sys.version_info >= (3, 0):
    raw_input = input

file_name = raw_input("Enter a file name: ")  # 选择一个文件
count = 0
t_char = 0

try:
    with open(file_name) as f:
        count = (sum(1 for line in f))
        f.seek(0)
        t_char = (sum([len(line) for line in f]))
except FileNotFoundError as e:
    print(e)
    sys.exit(1)
# python2的异常处理
except IOError:
    pass
#python3的异常处理
except IsADirectoryError:
    pass

file_stats = os.stat(file_name)
file_info = {
    'fname': file_name,
    'fsize': file_stats[stat.ST_SIZE],
    'f_lm': time.strftime("%d/%m/%Y %I:%M:%S %p",
                          time.localtime(file_stats[stat.ST_MTIME])),
    'f_la': time.strftime("%d/%m/%Y %I:%M:%S %p",
                          time.localtime(file_stats[stat.ST_ATIME])),
    'f_ct': time.strftime("%d/%m/%Y %I:%M:%S %p",
                          time.localtime(file_stats[stat.ST_CTIME])),
    'no_of_lines': count,
    't_char': t_char
}
# print out the file info
file_info_keys = ('文件名', '文件大小', '最后修改', '最后访问',
                  '创建日期', '总行数',
                  '总字符数')
file_info_vales = (file_info['fname'], str(file_info['fsize']) + " bytes",
                   file_info['f_lm'], file_info['f_la'], file_info['f_ct'],
                   file_info['no_of_lines'], file_info['t_char'])

for f_key, f_value in zip(file_info_keys, file_info_vales):
    print(f_key, ' =', f_value)

# check the `file` is direcotry
# print out the file stats
if stat.S_ISDIR(file_stats[stat.ST_MODE]):
    print("This a directory.")
else:
    file_stats_fmt = ''
    print("\nThis is not a directory.")
    stats_keys = ("st_mode (protection bits)", "st_ino (inode number)",
                  "st_dev (device)", "st_nlink (number of hard links)",
                  "st_uid (user ID of owner)", "st_gid (group ID of owner)",
                  "st_size (file size bytes)",
                  "st_atime (last access time seconds since epoch)",
                  "st_mtime (last modification time)",
                  "st_ctime (time of creation Windows)")
    for s_key, s_value in zip(stats_keys, file_stats):
        print(s_key, ' =', s_value)
```

## 脚本演示

![image-20201207205810485](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201207205810485.png)

<!-- more -->