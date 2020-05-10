---
title: PyCharm连接教程
date: 2020-04-08 17:45:55
tags:
---

社区版的 pycharm 不支持远程连接服务器的功能，需要使用专业版

[官网学生认证免费获得专业版](https://www.jetbrains.com/zh-cn/community/education/#students)

首先配置 Pycharm 服务器的代码同步，打开最上方工具栏处的 Tools -> Deployment ->  
Configuration，在弹出的窗口处点击左边的 + 添加一个部署配置，输入配置名 Name，Type 选择  
SFTP，然后确认。

{% asset_img 1.png %}

配置远程服务器的 IP，端口，用户名和密码，Root Path 是项目文件在远程服务器中的根目录

以下面的一条 ssh 命令为例：

ssh mist@47.103.52.232 -p 56771

用户名（user name）为 mist，ip(host) 为 47.103.52.232，端口（port）为 56771，密码(Password)是创建服务器时填写的。

Root path 则需设置成服务器根目录 /home/mist

{% asset_img 2.png %}

进入settings中的这一页面，进入python interpreter，如图更改project interpreter为远程服务器中的python

服务器的python路径在 /usr/local/bin/python

点击 Mappings，将 Local Path 设置为 Windows 下的工程目录，例如  
D:\Projects\ML-Project，自己视情况设定。将 Deployment path on server 设置为远程服务器中的项目目录
（上图中的是还未更改的状态）

点击 Excluded Paths 可以设置一些不想同步的目录，例如软件的配置文件目录等。

另外打开 Tools -> Deployment -> Options，将 Create Empty directories  
打上勾，要是指定的文件夹不存在，会自动创建。

{% asset_img 3.png %}

在pycharm左侧的项目管理窗口中，右键菜单deployment中点击sync，即可将项目文件夹中的所有文件同步到云服务器。请注意，如果不设置exclude path
或者清理掉旧的权重文件、数据集的话，上传时间将会非常长。考虑到整个上传过程都需要服务器开机，如果数据集非常庞大，建议先压缩
然后使用云存储功能进行上传，再开机服务器并解压。