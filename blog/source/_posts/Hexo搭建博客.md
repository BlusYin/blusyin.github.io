---
title: Hexo搭建博客
date: 2020-11-27 18:18:03
tags:
description: 介绍如何使用hexo搭建个人博客并部署到github pages上
---

# Step1: 安装必备的软件

## 安装nodejs,npm

### ArchLinux

```shell
sudo pacman -S nodejs npm
```

### 其他系统

自行去官网安装https://nodejs.org/, 注意，官网把npm和nodejs放在一个包里了，安装nodejs的同时也会安装npm

### 验证

```shell
$ node -v
$ npm -v
```

## 安装Hexo

```shell
$ npm install -g hexo-cli # -g表示从git仓库中安装
```

库地址https://github.com/hexojs/hexo

# Step2: 配置hexo环境

## 创建博客

进入一个合适的路径，输入命令：

```shell
$ hexo init blog
```

之后会生成一个blog文件夹，里面就是你的博客了

## 测试博客

进入该路径，输入以下命令：

```shell
$ cd blog
$ hexo generate # 生成静态网页
$ hexo server	# 启动本地服务
```

完成后打开浏览器输入地址https://localhost:4000, 浏览新创建的博客

## 创建一篇博文

```shell
$ hexo new "title"
```

这会在`source/_posts/`路径下生成一个markdown文件，打开进行编辑，输入博文内容并保存，再输入以下命令：

```shell
$ hexo g
$ hexo s
```

打开网页进行预览

# Step3: 部署网页

以部署到github pages上为例。

## 创建github pages

参考 https://pages.github.com/ 

## 关联hexo和仓库

复制你的github pages库的URL，打开`_config.yml`文件，找到`deploy:`这一行，将该行和它后面的内容修改为如下形式

```shell
deploy:
	type: 'git'
	repo: '<repo_url>'
	branch: '<branch>'
```

其中`<repo_url>`表示要填写库url，`<branch>`为该库的一个分支。

## 部署

在部署之前还要安装一个组件

```shell
$ npm install hexo-deployer-git --save
```

输入以下命令进行部署

```shell
$ hexo d
```

打开浏览器，输入github pages的url进行查看。

# END