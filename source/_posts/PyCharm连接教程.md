---
title: PyCharm连接教程
date: 2020-04-08 17:45:55
tags:
---

社区版的 pycharm 不支持远程连接服务器的功能，需要使用专业版

[官网学生认证免费获得专业版](https://www.jetbrains.com/zh-cn/community/education/#students)

首先配置 Pycharm 服务器的代码同步。打开最上方工具栏处的 Tools -> Deployment ->
Configuration，点击弹出窗口的左上角 + 并选择 SFTP 添加部署配置。配置名随意。

{% asset_img pyc_1.png %}

点击图示位置的三个点添加 SSH 配置

{% asset_img pyc_2.png %}

从[**控制台**](https://mistgpu.com/user/)中的 ssh 命令一栏中获取服务器地址，例如

`ssh mist@gpu28.mistgpu.com -p 10000`

将 mist 填入 User name 一栏，

gpu28.mistgpu.com 填入 Host 一栏，

10000 填入 port 一栏，

Password 是创建服务器时设置的密码。

{% asset_img pyc_3.png %}

点击 Test Connection 提示成功后确认保存

Root path 点击 auto detect 即可，设置成 /home/mist

{% asset_img pyc_4.png %}

打开 Pycharm 设置，进入 Python interpreter，点击右上角三个点 -> 添加。

{% asset_img pyc_5.png %}

选择 SSH Interpreter ，在 Existing 中选择刚才配置的服务器，下一步。

{% asset_img pyc_6.png %}

如图，更改 project interpreter 为 /usr/bin/python3 ，

Sync folders 将 Local Path 设置为自己电脑的工程目录，Deployment path 设置为远程服务器中的工程目录，完成。

{% asset_img pyc_7.png %}

之后，点击 Tools -> Deployment -> Options，将 Create Empty directories 打上勾。之后要是指定的文件夹不存在，会自动创建。

{% asset_img pyc_8.png %}

在项目页中，点击右键 Deployment 中 upload ，即可将项目文件夹中的所有文件同步到云服务器。

{% asset_img pyc_9.png %}

同步之后直接右击代码编辑页，点击 run 运行即可。

请注意，如果不设置 exclude path 或者清理掉旧的权重文件、数据集的话，上传时间可能很长。考虑到整个上传过程都需要服务器开机，如果数据集非常大，建议先压缩，然后点网站左边上传文件上传到云存储，再开机服务器并解压。

{% asset_img pyc_10.png %}

如果程序需要命令行参数，则点击 Tools -> Start SSH Session，出现 `mist@` 字样即表示已连接到服务器的命令行。
