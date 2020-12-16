---
title: 迁移hexo + github博客工作区
category: 
- 编程开发
tags: 
- github
---

## 什么情况下我们需要迁移我们的博客工作站

最近要放寒假了，外面冷的不行。我平常的作业以及大多数空余时间都在实验室，因此我的许多文件包括这个hexo博客的源文件以及环境啥的都在实验室的电脑上。那么就有一个很重要的问题，一旦这台电脑出现问题，而你有没有即使备份那我就白折腾了。因此 就有必要在我的笔记本上同步我的博客工作区间。

## 怎样迁移

### 首先

首先肯定是涉及到环境问题，我的博客是使用hexo + githubpages的方式，所以基本的环境还是很容易搭建的：

1. 安装node
2. 安装hexo
3. 安装gitbash

这里贴一下我自己的版本信息:

![image-20201216210239287](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201216210239287.png)

尽量使用一样的开发环境，比如你原来电脑上是node14那你接下来就继续用node14。

### 其次

安装好环境后，使用git 连接你的仓库。并添加远程源。

```
git config --global user.name 'your_name'
git config --global user.email 'your_email'  //配置用户名和邮箱
ssh-keygen -t rsa -C 'your_email'		//生成你的rsakey
ssh git@github.com					//测试是否有权访问你的github库
git init 						//初始化git仓库
```

接下来就很关键了。你可以选择`git clone`ba把你的远程库的内容拉取下来 ，然后同步你的本地库与远程库。但我推荐另一种：

直接复制你原来电脑上的本地仓库，打包成压缩包。在你的新电脑上解压他然后复制所有的文件放到你新建的本地仓库中。然后执行以下命令即可同步你的远程库以及本地库。

```
git status 
git add .
git commit "xxxxxx"
git pull origin master
git push prigin master
```

这些命令都是比较基础的给i他命令，作用就是把你的本地仓库与你的远程库合并，并提交到远程库：

执行完成后大概是这样：

### ![image-20201216213259444](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201216213259444.png)

其实说到底还是挺简单的，但是网上教程那么多我是真的人都找麻了没找到个可用的。关键就是你不能改变你远程库原有的状态。希望对你有帮助。

## 演示

上面步骤都做好后可以hexo - s 一下，看看本地效果是不是和云端一致，如果是的说明没毛病。

<!-- more -->