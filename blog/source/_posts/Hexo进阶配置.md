---
title: Hexo进阶配置
date: 2020-11-27 18:18:09
tags:
description: 关于hexo的更多配置
---

# 更改主题

https://hexo.io/themes/, 这里有很多主题。这里以安装next主题为例，主题仓库https://github.com/next-theme/hexo-theme-next

## 安装next主题

首先进入到博客的根目录，输入命令

```shell
$ npm install hexo-theme-next
```

## 修改配置

打开`_config.yml`文件，找到`theme:` 这一行，将主题修改为next：

```yml
theme: next
```

## 重新生成网页

```shell
$ hexo g
$ hexo s
```

打开 https://localhost:4000 进行预览

# 显示图片

Hexo自带了这一功能，但需要修改配置文件以启用。打开`_config.yml`文件，找到`post_asset_folder: false`这一行，将`false`改为`true`:

```shell
post_asset_folder: true
```

还要安装一个组件

```shell
$ npm install hexo-asset-link
```

配置完成！

之后每次使用`hexo n`创建博文都会在`source/_post/`路径下生成一个和博文title同名的文件夹，将图片放在该文件夹下，在markdown文件中使用相对路径引用图片，编辑完后使用命令`hexo g`生成的静态网页就能正常显示图片了。

# END