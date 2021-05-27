---
title: python基础防走丢
category: 
- 编程
tags: 
- python
---

## python基础

### 数据类型和变量

python可以直接处理的**数据类型**：

- 整数
- 浮点数
- 字符串
- 布尔值
- 空值
- 自定义数据类型：list tuple dict ...

python**变量**本身类型不固定，因此也叫它**动态**语言：

- 变量：定义变量时不必指定变量类型
- 常量：在Python中，通常用全部大写的变量名表示常量（只是一个习惯上的用法）

### 字符串和编码

python[字符编码](https://www.liaoxuefeng.com/wiki/1016959663602400/1017075323632896)的问题（经常遇到）：贴一下廖老师的解释，一目了然。

- python3中：字符串是以Unicode编码的。

[^1]: 在操作字符串时，我们经常遇到`str`和`bytes`的互相转换。为了避免乱码问题，应当始终坚持使用UTF-8编码对`str`和`bytes`进行转换。由于Python源代码也是一个文本文件，所以，当你的源代码中包含中文的时候，在保存源代码时，就需要务必指定保存为UTF-8编码。当Python解释器读取源代码时，为了让它按UTF-8编码读取，我们通常在文件开头写上这两行：

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-
```

- 格式化输出：python使用占位符格式化字符。

<!-- more -->

![image-20210208205715420](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20210208205715420.png)

```python
print('Hi, %s, you have $%d.' % ('Michael', 1000000))
```

### 使用list 和tuple注意

- [list](https://www.liaoxuefeng.com/wiki/1016959663602400/1017092876846880) 规范使用：
- [tuple](https://www.liaoxuefeng.com/wiki/1016959663602400/1017092876846880) 注意事项：tuple和list非常类似，但是tuple一旦初始化就不能修改。(这里的不变是 指向不变 具体看链接)

[^]: 不可变的tuple有什么意义？因为tuple不可变，所以代码更安全。如果可能，能用tuple代替list就尽量用tuple。tuple的陷阱：当你定义一个tuple时，在定义的时候，tuple的元素就必须被确定下来。

```python
 t = (1, 2)
 #(1, 2)
```

### 条件判断（略）

### [循环](https://www.liaoxuefeng.com/wiki/1016959663602400/1017100774566304)

### 使用dict 和set 注意

- [dict](https://www.liaoxuefeng.com/wiki/1016959663602400/1017104324028448):

[^]: dict可以用在需要高速查找的很多地方，在Python代码中几乎无处不在，正确使用dict非常重要，需要牢记的第一条就是dict的key必须是**不可变对象**。这是因为dict根据key来计算value的存储位置，如果每次计算相同的key得出的结果不同，那dict内部就完全混乱了。这个通过key计算位置的算法称为哈希算法（Hash）。要保证hash的正确性，作为key的对象就不能变。在Python中，字符串、整数等都是不可变的，因此，可以放心地作为key。而list是可变的，就不能作为key：

```python
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unhashable type: 'list'
```

<!-- more -->