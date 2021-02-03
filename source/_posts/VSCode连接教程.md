---
title: VSCode连接教程
date: 2021-02-01 14:00:00
tags: VSCode
---

首先从[VSCode官网](https://code.visualstudio.com/download)下载并安装VSCode。

打开软件后可参考图示，先在插件中安装中文语言包，方便操作。

{% asset_image 1.png %}

之后继续在插件中输入`Remote-ssh`安装ssh插件。

{% asset_image 2.png %}

进入远程资源管理器，鼠标移到`SSH Targets`上时会出现一个加号，点击加号并输入SSH命令。

{% asset_image 3.png %}

SSH命令可以在[控制台](https://www.mistgpu.com/user/)中点击复制。(服务器必须为开机状态才可以连)

{% asset_image 4.png %}

出现这个框直接回车即可，SSH配置信息将保存到提示的文件中。

{% asset_image 5.png %}

完成后点击`Host Added`中的`Connect`，或将鼠标移到远程资源管理器的服务器中，点击在新窗口中打开。

{% asset_image 6.png %}

出现这个框提示选择远程主机平台类型，请点击选择`Linux`或默认回车。

{% asset_image 7.png %}

之后这个提示接受服务器密匙，选择`continue`或默认回车。

{% asset_image 8.png %}

最后输入创建服务器时设置的密码，回车就完成了。

{% asset_image 9.png %}

连接成功后在资源管理器中点击`打开文件夹`，选择实际项目的文件夹即可。本例中所有项目文件都在`/home/mist/project`下，请以实际为准。

{% asset_image 10.png %}

之后就可以在资源管理器中查看到服务器上的文件了，点击`py`文件若提示需要安装python拓展则直接点击安装即可。
最后点击右上角的三角运行图标就可以运行了，如需调试请参考[官方文档](https://code.visualstudio.com/docs/python/debugging)配置。

{% asset_image 11.png %}

当前GPU占用和显存占用等信息可以在终端用`py3smi`命令查看。
: 使用`pip install py3nvml --user`安装
