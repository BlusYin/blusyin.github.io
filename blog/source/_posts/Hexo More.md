---
title: 关于Hexo的配置
date: 2020-11-27 18:18:09
excerpt: 搭建一个完整的博客网站
categories:
- Hexo
tags:
- Blog
---

> The only thing that will never change is change.
>
> 永远不变的是改变

当你着手完善你的Hexo博客时，不妨先看看官方文档https://hexo.io/docs/

## 更改主题

可以到hexo的官方网站https://hexo.io/themes/查看，有很多主题可供选择。这里以安装next主题为例，主题仓库https://github.com/next-theme/hexo-theme-next

首先进入到博客的根目录，下载next主题仓库：

```shell
$ git clone https://github.com/next-theme/hexo-theme-next themes/next
```

然后打开`_config.yml`文件，找到`theme:` 这一行，将主题修改为next：

```yml
theme: next
```

重新生成网页

```shell
$ hexo g
$ hexo s
```

打开 https://localhost:4000 进行预览

## 设置分类和标签

### 为博文设置分类和标签

#### 分类

在front-matter中添加categories这一项，后面填具体分类（换行写）：

```yaml
categories:
- 类别一
- 类别二
- [<类别三>, <小类1>, <小类2>, ...]  #  二级分类
```

Hexo不支持三级及以上的分类

#### 标签

在front-matter中添加tags这一项，后面填具体标签（换行写）：

```yaml
categories:
- 标签一
- 标签二
```

### 生成分类和标签页面

首先通过执行以下命令生成categories和tags这两个page：

```shell
$ hexo new page "categories"
$ hexo new page "tags"
```

source目录下会产生两个目录categories和tags，里面有一个index.md文件，通过编辑该文件即可修改这两个页面的显示。

> 分类和标签页面的名称是由`_config.yml`配置指定的（tag_dir和category_dir这两项），可以在配置文件中修改以指定其他名称。

### 显示分类和标签页面的入口

这个需要修改主题配置文件，以Next主题为例，打开主题配置文件，找到Menu Settings，将tags和categories这两项取消注释。

## 显示图片

Hexo自带了这一功能，但需要修改配置文件以启用。打开`_config.yml`文件，找到`post_asset_folder: false`这一行，将`false`改为`true`:

```shell
post_asset_folder: true
```

还需要安装`hexo-asset-link`：

```shell
$ npm install hexo-asset-link
```

配置完成！

之后每次使用`hexo n`创建博文都会在`source/_post/`路径下生成一个和博文title同名的文件夹，将图片放在该文件夹下，在markdown文件中使用相对路径引用图片，编辑完后使用命令`hexo g`生成的静态网页就能正常显示图片了。

## 在主页显示摘要

编辑主题配置文件`theme/next/_config.yml`, 加入`excerpt_discription: true`(next主题默认已经启用了)

在markdown的front-matter中加入`excerpt: `，在后面添加摘要。

## 段落自动缩进

修改主题的CSS样式，在段落的样式中添加`text-indent: 2em;`这一项。

```css
p {
  text-indent: 2em;
}
```

next主题的base style在*source/css/_common/scaffolding/base.styl*文件中。

## 修改显示语言

修改配置文件`_config.yml`，将`language: `后面修改为`zh-CN`。

## END