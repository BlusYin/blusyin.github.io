---
title: Hexo搭建博客
date: 2020-11-27 18:18:03
excerpt: 介绍如何使用hexo搭建个人博客并部署到github pages上
categories:
- Hexo
tags:
- Blog
---

>  Get busy living, or get busy dying
>
> 要么忙着活，要么忙着死

## Step1: 安装必备的软件

### 安装nodejs,npm

可以使用系统的包管理器进行安装

```shell
$ sudo pacman -S nodejs npm
```

也可以去官网https://nodejs.org/下载源码，然后编译安装。 注意，官网把npm和nodejs放在一个包里了，安装nodejs的同时也会安装npm

#### 验证

```shell
$ node -v
$ npm -v
```

### 安装Hexo

```shell
$ sudo npm install -g hexo-cli # -g表示系统范围的安装
```

> 如果不添加`-g`参数，npm默认会将软件包安装在当前目录的`node_modules`目录下，并把可执行文件放到`node_modules/.bin`目录下。（全局安装需要root权限）

## Step2: 配置hexo环境

### 创建博客

进入一个合适的路径，输入命令：

```shell
$ hexo init blog
```

之后会生成一个blog文件夹，blog就是博客的根目录。

### 测试博客

进入博客的根目录，输入以下命令：

```shell
$ cd blog
$ hexo generate # 生成静态网页
$ hexo server	# 启动本地服务
```

完成后打开浏览器输入地址https://localhost:4000, 浏览新创建的博客

可以随时通过`hexo clean`命令清除已经生成的静态网页。

如果hexo server无法运行，则需要安装一个hexo-server组件：

```shell
$ npm install hexo-server
```

> 有些比较旧的博客会带`--save`这个参数，表示将已经安装的包作为依赖添加到package.json文件中，这个设置现在默认是启用的，所以可以不用指定`--save`参数。

### 创建一篇博文

```shell
$ hexo new "title"
```

这会在`source/_posts/`路径下生成一个markdown文件，打开进行编辑，输入博文内容并保存，再输入以下命令：

```shell
$ hexo g	# hexo generate
$ hexo s	# hexo server
```

打开网页进行预览

## Step3: 部署网页

以部署到github pages上为例。

### 创建github pages

参考 https://pages.github.com/ 

### 关联hexo和仓库

复制你的github pages库的URL，打开`_config.yml`文件，找到`deploy:`这一行，将该行和它后面的内容修改为如下形式

```shell
deploy:
	type: 'git'
	repo: '<repo_url>'
	branch: '<branch>'
```

其中`<repo_url>`表示要填写库url，`<branch>`为该库的一个分支(默认为master)

> 将\<repo_url>设置为ssh类型的github库地址即可通过ssh免密部署

### 部署

在部署之前还要安装一个包

```shell
$ npm install hexo-deployer-git
```

输入以下命令进行部署

```shell
$ hexo d	# hexo deploy
```

打开浏览器，输入github pages的url进行查看。

## END