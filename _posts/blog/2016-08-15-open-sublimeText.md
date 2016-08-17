---
layout:     post
title:      在windows系统上添加右键“Sublime Text”的打开方式
description: 在windows系统上添加右键“Sublime Text”的打开方式
categories: blog
tags: 实用操作
---

Sublime Text 安装完成后没有右键打开的方式，Atom编辑器安装完成后有右键打开文件。为了快捷打开文件，可修改注册表添加 Sublime Text 打开方式，如图所示。

![img](/images/upload/sublime/1.png)

1、打开注册表编辑器

开始 --> 运行，输入regedit。

![img](/images/upload/sublime/2.png)


2、查找节点

 * 不同的 .* 后缀文件的右键的效果（单个文件） [ HKEY_CLASSES_ROOT --> * --> Shell  ]
![img](/images/upload/sublime/3.png)

 * 在Shell下，新建项命名为Sublime Text 3，并新建字符串值，名称“Icon”，值“C:\Program Files\Sublime Text 3\sublime_text.exe”（使用实际的安装文件目录）
![img](/images/upload/sublime/4.png)

 * 在Sublime Text 3项下面新建项command，修改右侧窗口的默认值，修改为[ "C:\Program Files\Sublime Text 3\sublime_text.exe" "%1" ] （使用实际的安装文件目录）
![img](/images/upload/sublime/5.png)

 *  文件夹的右键的效果（单个文件） [ HKEY_CLASSES_ROOT --> Directory --> Shell  ]同上的操作
![img](/images/upload/sublime/6.png)

不用重启，找文件右键单击可看到有Sublime Text的打开方式了！文件夹也可。          
        


