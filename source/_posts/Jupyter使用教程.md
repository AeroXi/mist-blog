---
title: Jupyter使用教程
date: 2022-11-26 12:00:00
tags:
---

# 概述

Jupyter Lab中集成开发环境，可以用户编写代码、运行notebook(*.ipynb文件)、操作服务器终端，以及上传/下载文件等功能。

在控制台开机后点击左下角的“进入环境”按钮即可进入服务器的Jupyter环境。

# 界面介绍

打开Jupyter后界面如下图所示，启动页可以点击左上角蓝色底的加号图标弹出。

{% asset_img jupyter1.png %}

# 浏览/下载文件

在Jupyter左侧文件管理器中可以看到服务器中的文件。可双击打开文件，或右键下载。

{% asset_img jupyter4.png %}

> 由于Jupyter底层冲突，名为`checkpoints`的文件夹无法打开/删除。请手动重命名为其他名称(如`checkpoint`)或到服务器终端中访问

在文件管理器中进入项目目录后，通过启动页启动服务器终端时会自动将终端的当前路径设置为此目录。

{% asset_img jupyter5.gif %}

在终端中输入`pwd`命令即可看到此目录的绝对路径，其他终端操作请参考[终端使用教程](http://blog.mistgpu.com/2022/11/21/%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%BB%88%E7%AB%AF%E4%BD%BF%E7%94%A8%E6%95%99%E7%A8%8B/#%E5%B8%B8%E7%94%A8%E7%BB%88%E7%AB%AF%E6%93%8D%E4%BD%9C)。

# Notebook 文件

`*.ipynb`文件在Jupyter中可直接运行

> 注意notebook中执行的是Python代码而不是Linux终端代码

> 简要Linux命令可以在命令头加英文感叹号执行，比如`nvidia-smi`

{% asset_img jupyter2.png %}

一般不太建议在notebook中长时间执行程序，因为当单元格内输出变多后Jupyter本身速度会变慢，且刷新页面后实时输出可能不会保存。
若需要长时间运行，请点击菜单栏`文件`-`将notebook另存为`，将拓展名改为`.py`后到服务器终端运行。

{% asset_img jupyter3.png %}

# Python 文件

`*.py`文件在Jupyter中只可编辑，不可直接运行。如需运行`.py`文件请使用服务器终端执行。具体请参考[终端使用教程](http://blog.mistgpu.com/2022/11/21/%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%BB%88%E7%AB%AF%E4%BD%BF%E7%94%A8%E6%95%99%E7%A8%8B/#%E8%BF%90%E8%A1%8Cpy%E4%BB%A3%E7%A0%81)

# 服务器终端

在启动页点击黑色的终端，或在`文件`-`新建`中选择终端。

> 注意是黑色的终端`Terminal`，而不是蓝色的`Console`

{% asset_img jupyter6.png %}

在Jupyter终端内，**选中文本**后`Ctrl-c`可复制，`Ctrl-v`可粘贴。
> 不选中文本按`Ctrl-c`会中断正在操作的命令

具体终端操作命令请移步[终端使用教程](http://blog.mistgpu.com/2022/11/21/%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%BB%88%E7%AB%AF%E4%BD%BF%E7%94%A8%E6%95%99%E7%A8%8B/#%E5%B8%B8%E7%94%A8%E7%BB%88%E7%AB%AF%E6%93%8D%E4%BD%9C)。
