---
title: PyCharm连接教程
date: 2021-02-01 16:00:00
tags: PyCharm
---
# 前言

本教程基于最新PyCharm 2021.3 Professional专业版，Community社区版不支持连接到远程服务器，故无法使用。

[官网学生认证可免费获得专业版链接](https://www.jetbrains.com/zh-cn/community/education/#students)

# 特别说明

PyCharm是调试代码的工具，若代码需要长时间运行，请参考[SSH连接教程](http://blog.mistgpu.com/2021/02/03/SSH%E8%BF%9E%E6%8E%A5%E6%95%99%E7%A8%8B/)，在服务器终端中使用`screen`将代码挂到后台运行。

***
# 安装中文包
PyCharm已有中文语言包，可在`PyCharm设置 - Plugins`中搜索并安装，随后重启PyCharm即可生效。

{% asset_img pyc-1.png %}

***
# 添加SSH解释器

打开项目后点击右下角的`Python解释器`选项并点击`添加解释器`。
也可以在`PyCharm设置 - 项目 - Python解释器`里点击右上角的齿轮图标添加。

{% asset_img pyc-2.png %}

在添加Python解释器页面请务必选择左边的`SSH 解释器`，右边具体信息可前往**控制台-附加功能-使用帮助-服务器连接信息**中查看。

{% asset_img pyc-3.png %}

{% asset_img pyc-4.png %}

添加时请确保服务器为开机状态，密码同SSH连接密码，为创建服务器时设置的。

{% asset_img pyc-5.png %}

初次连接服务器时会提示是否确认指纹，点击“是”即可。

{% asset_img pyc-6.png %}

下一步中需要修改解释器的路径(绿色箭头处)

- 若使用默认环境，**必须在此处最后加上3**，变成`/usr/local/bin/python`。否则找不到预装的包。
- 若使用conda虚拟环境，则需要替换为**实际解释器路径**。详见[conda教程](http://blog.mistgpu.com/2021/02/03/Conda%E8%99%9A%E6%8B%9F%E7%8E%AF%E5%A2%83/#%E5%9C%A8PyCharm%E4%B8%AD%E4%BD%BF%E7%94%A8conda%E5%88%9B%E5%BB%BA%E7%9A%84%E7%8E%AF%E5%A2%83)

{% asset_img pyc-7.png %}

之后点击“同步文件夹”右边的文件夹图标，将右边远程路径改为服务器主目录`/home/mist`下。

> 请务必修改到主目录下，默认使用的`/tmp/`目录会在每次关机后清空。

设置完成后检查Python版本与路径映射，无误点击右下角“确认”即可
{% asset_img pyc-8.png %}

# 设置部署

完成后在Pycharm会创建服务器环境索引，大约需要`2-5`分钟。

{% asset_img pyc-9.png %}

同时右下角会弹出“已创建到服务器的部署配置”，点击红色箭头`配置`。

> 也可到Pycharm设置-“构建-执行-部署”-部署中设置

{% asset_img pyc-10.png %}

在“连接”一栏中需要做以下设置
1. 点击“测试连接”按钮，确认Pycharm可以连接到服务器
2. 点击根路径右边的“自动检测”按钮，或手动将根路径设置为`/home/mist`
3. 若使用`macOS`或`Linux`系统，可在“高级”下勾选“使用rsync下载或上传”。`Windows`系统不支持，无需勾选。

> rsync支持断点续传，旧版本Pycharm中无此功能。

> Windows可手动安装，具体可见[官方文档](https://www.jetbrains.com/help/pycharm/settings-tools-rsync.html)

4. 将“通信编码”改为`UTF-8`

之后进入“映射”一栏，将部署路径设置为`/`

> 若在服务器主目录下创建了子文件夹，则填 `/文件夹名`

> web路径可不填
> 
{% asset_img pyc-11.png %}


由于PyCharm会自动上传项目文件夹内所有的文件，若项目里含大数据集的话上传时间会很长。
建议进入`排除的路径`一栏，点击`添加排除的路径 - 本地路径`。添加后的文件/文件夹PyCharm将不会自动上传。

{% asset_img pyc-12.png %}

数据集可到[上传数据集](https://www.mistgpu.com/upload/)中手动上传，
之后再解压到服务器中(可使用蓝色箭头所指的 `unzip` 命令)。

{% asset_img pyc-13.png %}

# 完成

保存后配置就完成了，运行或调试与使用本地环境均无区别。

> Pycharm是编写/调试代码的工具，若程序需要长时间运行，请**务必**使用终端并挂到后台执行。详情可见[常见问题](https://www.mistgpu.com/faq/)

{% asset_img pyc-14.png %}

***
# 附加
## 在PyCharm中使用SSH连接

若需要在终端中操作，可在菜单栏中的`工具 - 启动SSH会话`连接到服务器终端。如边训练边使用`watch nvidia-smi`命令监控GPU实时占用情况。[常用终端操作](http://blog.mistgpu.com/2021/02/03/SSH%E8%BF%9E%E6%8E%A5%E6%95%99%E7%A8%8B/#%E5%B8%B8%E7%94%A8%E6%93%8D%E4%BD%9C)

{% asset_img pyc-15.png %}

上图红框部分为显存使用情况，蓝框部分为GPU资源整体占用情况。

## 浏览服务器上的文件或下载到本地

训练生成的文件都会保存在服务器上，可以点击`远程主机`并找到所需要的文件，右键点击就可以下载到自己的电脑上了。
若找不到`远程主机`，则需要在`工具(Tools)菜单栏`中找到`部署(Deployment)`后点击`浏览远程主机(Browse remote host)`。

{% asset_img pyc-16.png %}

***
## 修改配置参数
最后，如果运行的程序需要从命令行获取参数，可以修改配置文件。

比如在命令行中要求使用`python3 train.py --mode train --epoch 50`，则在参数一栏加上参数部分即可。

{% asset_img pyc-17.png %}

# 常见问题
## 找不到文件

找不到文件的提示信息如下图：说明服务器上无该文件。
> 若蓝色框内的路径为本地路径，例如`D:\Folder\file.py`，说明路径设置有误。

{% asset_img pyc-18.png %}

此时可以在代码空白处右键，在部署中手动点击上传。

## 缺包 / 刚装完的包依然爆红

一般刚装完包后Pycharm不会立即更新解释器索引，此时可以直接运行程序。或程序没有抛出`ImportError`的异常即不影响，重启Pycharm即可让Pycharm强制更新索引。

{% asset_img pyc-19.png %}

若使用默认环境且`torch`、`tensorflow`、`numpy`等预装的包仍提示`ImportError`，则需检查右下角Python解释器版本是否为默认`3.6.9`

## PyQt等报错

通过SSH运行程序是无法激活窗口，PyQt会报错
> `qt.qpa.xcb: could not connect to display` 

如程序需要图形界面弹出窗口，请连接到图形界面([教程](http://blog.mistgpu.com/2021/04/19/%E5%9B%BE%E5%BD%A2%E7%95%8C%E9%9D%A2%E8%BF%9E%E6%8E%A5%E6%95%99%E7%A8%8B/))，并在**远程桌面内**启动终端运行程序。