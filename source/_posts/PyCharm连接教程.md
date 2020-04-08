---
title: PyCharm连接教程
date: 2020-04-08 17:45:55
tags:
---

Pycharm连接服务器
=================

首先，社区版的pycharm尚不具备远程连接服务器的功能，需要使用专业版。

首先配置 Pycharm 服务器的代码同步，打开最上方工具栏处的 Tools -\> Deployment -\>
Configuration，在弹出的窗口处点击左边的 + 添加一个部署配置，输入配置名 Name，Type 选择
SFTP，然后确认。

{% asset_img 1.png %}

配置远程服务器的 IP，端口，用户名和密码，Root Path
是项目文件在远程服务器中的根目录

以下面的一条ssh命令为例：

ssh mist\@47.103.52.232 -p 48744 

ip为47.103.52.232，端口为48744，用户名为mist，密码在创建服务器时确定。

Root path则需设置成/home/mist/下您自己项目的文件夹。

{% asset_img 2.png %}

点击 Mappings，将 Local Path 设置为 Windows 下的工程目录，例如
D:\\Projects\\ML-Project，自己视情况设定。将 Deployment path on server
设置为远程服务器中的项目目录

点击 Excluded Paths 可以设置一些不想同步的目录，例如软件的配置文件目录等。

另外打开 Tools -\> Deployment -\> Options，将 Create Empty directories
打上勾，要是指定的文件夹不存在，会自动创建。
