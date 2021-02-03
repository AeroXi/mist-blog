---
title: PyCharm连接教程
date: 2021-02-01 16:00:00
tags: PyCharm
---
# 前言
本教程仅适用于专业版PyCharm，社区版不支持远程连接服务器。

[官网学生认证免费获得专业版](https://www.jetbrains.com/zh-cn/community/education/#students)

***
# 安装中文包
PyCharm已有中文语言包，可在`PyCharm设置 - Plugins`中搜索安装，重启PyCharm即可生效。

{% asset_img 1.png %}

***
# 添加SSH解释器
在PyCharm打开项目后点击右下角的`Python解释器`选项并点击`添加解释器`。
也可以在`PyCharm设置 - 项目 - Python解释器`里点击右上角的齿轮图标添加。

{% asset_img 2.png %}

在添加Python解释器页面选择左边的`SSH 解释器`，将服务器信息填入即可。

{% asset_img 3.png %}

{% asset_img 4.png %}

主机名为图示篮筐部分，端口为绿框部分，添加时请确保服务器为开机状态。
如不确定也可以点击红箭头指的使用帮助查看。

下一步中在`解释器`一栏(蓝框)的最后加上3，变成`/usr/bin/python3`

{% asset_img 5.png %}

同步文件夹可点击右边的文件夹图标配置，将远程路径改为主目录(`/home/mist`)下。本实例的所有文件都放在`/home/mist/project/`下，请以实际为准。

{% asset_img 5-1.png %}
# 设置部署
完成后在右下角会弹出“已创建到服务器的部署配置”，点击`配置`。

{% asset_img 6.png %}

点击`根路径`右边的`自动检测`按钮，根路径应自动设置为`/home/mist/`。之后点击绿框中的`映射`

{% asset_img 7.png %}

点击部署路径右边的文件夹图标，选择项目地址，本实例中选择`project`。
注意由于之前已经设置过`根路径`了，因此`部署路径`中**不再需要**写/home/mist，直接写`/文件夹名`即可。
`Web路径`可不填。

{% asset_img 8.png %}

由于PyCharm会自动上传项目所需要的所有文件，因此如果项目里包括较大的数据集的话上传时间会很长。
建议进入`排除的路径`，点击`添加排除的路径 - 本地路径`。添加后的文件/文件夹PyCharm将不会自动上传。
如果数据及很大请先压缩成zip格式，到[上传数据集](https://www.mistgpu.com/upload/)中手动上传，
之后再手动解压到服务器中(参考蓝色框中的`unzip`命令)。

{% asset_img 9.png %}

# 完成
保存之后配置就完成了，运行和调试和在本地无区别，只要右下角显示的是远程SSH解释器就是在使用服务器的资源了。

{% asset_img 10.png %}
***
# 附加
## 在PyCharm中使用SSH连接
{% asset_img 11.png %}

之后还可以点击菜单栏中的`工具 - 启动SSH会话`连接到服务器，边训练边使用`watch py3smi`命令监控GPU使用情况
(如找不到此命令可使用`pip install py3nvml`安装)。
下图红框部分为显存使用情况，篮筐部分为GPU资源整体占用情况。
{% asset_img 12.png %}
## 从服务器上下载文件
训练生成的文件都会保存在服务器上，可以点击`远程主机`并找到所需要的文件，右键点击就可以下载到自己的电脑上了。
{% asset_img 13.png %}

***
## 修改配置参数
最后，如果运行的程序需要从命令行获取参数，可以修改配置文件。
{% asset_img 14.png %}
比如在命令行中要求使用`python3 train.py --mode train --epoch 50`，则在参数一栏加上参数部分即可。
{% asset_img 15.png %}