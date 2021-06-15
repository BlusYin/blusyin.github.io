---
title: ArchLinux下的Xfce桌面配置
date: 2021-06-14 18:55:53
tags: 
- Xfce
description: Xfce是一个基于GTK 3的轻量级模块化桌面，本文介绍Xfce桌面下的一些实用软件及其相关配置，以提高在Xfce桌面的工作效率
---

> 路漫漫其修远兮，吾将上下而求索

​		Xfce是一个基于GTK 3的轻量级模块化桌面，非常简洁，只提供窗口管理器，文件管理器，桌面和应用面板，不过这些都足够提供一个完整的用户体验了。

​		进入Xfce的桌面环境，下方是一个**居中面板**，有终端模拟器、文件管理器、网页浏览器等启动器；上方是一个**全宽面板**，面板最左边是应用菜单，右边就是一些小**组件**，如网络管理器、扬声器、电源、通知、日期和时间等，小组件的左边是**工作空间**的入口，默认有四个工作空间，我们现在就处在第一个工作空间，可以通过点击这些入口在不同的工作空间之间切换，面板剩余的部分用于存放已经打开的**窗口**。如下图所示：

![image-20210614200255235](Xfce Intro/image-20210614200255235.png)

​		Xfce简洁而且复古，不像KDE桌面那样现代化，也没有KDE那些强大的功能，窗口也不像KDE那样可以自己定制，但是却内置了一些非常使用的功能。不得不提到的就是下拉终端了。

> kde下的**关键字动作（keyword action）**是本人非常喜欢的一个功能，非常强大也非常好用

## 下拉终端

​		Xfce的终端模拟器`xfce4-terminal`默认就支持下拉功能，只需要执行`xfce4-terminal --drop-down`命令就可以打开这样一个下拉终端。为了更方便使用，当然还是要添加到快捷键了。点击右上角的Applications->Settings->Keyboard，在Application Shortcuts标签中添加，命令设置为`xfce4-terminal --drop-down --hide-menubar`，快捷键设置为\<F12>（可以根据个人喜好随意设置）。

## 截图、图片查看和编辑

​		Xfce内置的截图工具`xfce4-screenshooter`也非常好用，而且系统已经配置好了快捷键，*Print*键全屏截图，*Shift+Print*区域截图，*Alt+Print*截取当前窗口，可以在快捷键设置中进行查看和修改。图片查看和编辑分别用的Ristretto（Xfce项目）和mtPaint，都是非常轻量的应用。

## Synapse

​		Xfce内置的应用查找仅限于在添加到Applications菜单里的应用，要查找其他应用或者文档就不行了，所以我们需要synapse这个软件，不管是应用、文档还是网页都能检索。首先通过pacman安装synapse

```shell
$ sudo pacman -S synapse
```

​		将synapse添加到快捷键中，命令设置为`synapse`，快捷键为*Alt+\<F2>*（这个快捷键默认已经分配给了Xfce自带的搜索功能，需要先在快捷键设置中将它删掉或改成其他的）。

## 文档

​		Xfce自带了一个文本编辑器Mousepad，和gedit简直一模一样，功能也足够了，但界面不好看，也没有扩展。安装一个VScode用于日常开发（Atom也行）。PDF阅读器有很多，xreader足矣。Office的话就用libreoffice就好了。Markdown用Typora。

```shell
$ sudo pacman -S code xreader libreoffice-fresh   # libreoffice-fresh是稳定版
$ yay -S typora
```

## 中文输入法

​		安装fcitx5-im（包括fcitx5，fcitx5-configtool，fcitx5-gtk，fcitx5-qt等），fcitx5-chinese-addons。

```shell
$ sudo pacman -S fcitx5-im fcitx5-chinese-addons
```

​		在/etc/environment文件中添加如下内容：

```
GTK_IM_MODULE=fcitx
QT_IM_MODULE=fcitx
XMODIFIERS=@im=fcitx
```

​		将~/.config/fcitx5/profile修改如下：

```
[Groups/0]
# Group Name
Name=Default
# Layout
Default Layout=us
# Default Input Method
DefaultIM=pinyin

[Groups/0/Items/0]
# Name
Name=keyboard-us
# Layout
Layout=

[Groups/0/Items/1]
# Name
Name=pinyin
# Layout
Layout=

[GroupOrder]
0=Default
```

​		logout或者重启即可。通过*Ctrl+Space*快捷键切换到拼音输入。

## 其他问题

### 扬声器

​		安装完Xfce桌面后扬声器用不了，需要安装pavucontrol和pulseaudio这两个包：

```shell
$ sudo pacman -S pavucontrol pulseaudio
```

### 在其他窗口滚动鼠标后，当前窗口失去焦点

​		Applications->Settings->Window Manager Tweaks->Accessibility，取消勾选Raise windows when any mouse button is pressed。

