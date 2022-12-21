---
title: Pycharm配置教程
date: 2022-11-19 12:00:00
tags:
---

# 前言

本教程基于PyCharm 2022.2 Professional专业版，Community社区版不支持连接到远程服务器，故无法使用。

[官网学生认证可免费获得专业版链接](https://www.jetbrains.com/zh-cn/community/education/#students)

>
Pycharm2022.2版本debug代码时有[bug](https://youtrack.jetbrains.com/issue/PY-55448/Stop-script-on-remote-interpreter-hangs)
，如果有影响建议先[降级到2022.1版本](https://www.jetbrains.com/zh-cn/pycharm/download/other.html)使用

# 特别说明

PyCharm是调试代码的工具。若代码需要长时间运行，请到服务器终端中用screen挂到后台运行。具体可参考[终端使用教程](http://blog.mistgpu.com/2022/11/21/%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%BB%88%E7%AB%AF%E4%BD%BF%E7%94%A8%E6%95%99%E7%A8%8B/#%E5%B8%B8%E7%94%A8%E7%BB%88%E7%AB%AF%E6%93%8D%E4%BD%9C)
。

***

# 安装中文包

PyCharm已有中文语言包，可在`PyCharm设置 - Plugins`中搜索`Language Pack`并安装，随后重启PyCharm即可生效。

{% asset_img pyc1.png %}

# 配置SSH解释器(2022.2+)

打开项目后，进入Pycharm设置，选择`项目-Python解释器`并在`添加解释器`中选择`SSH`

{% asset_img pyc2.png %}

## 设置服务器信息

依次填入服务器域名、SSH端口。用户名固定为`mist`

{% asset_img pyc4.gif %}

- 如果没有私钥，则将创建服务器时设置的服务器密码填入密码框中并下一步
- 如果有私钥，则点击`密钥对`按钮，点击红框出的文件夹图标选择`.pem`私钥文件后下一步

{% asset_img pyc5.png %}

## 设置解释器路径

选择系统解释器后，点击解释器右边的三个点，找到解释器路径

{% asset_img pyc6.png %}

- 如果使用默认环境，则找到`/usr/local/bin/python`即可
- 如果使用conda虚拟环境，则需要找到**激活环境**后`which python`返回的路径，如下图所示

{% asset_img pyc7.png %}

## 设置同步文件夹

按下图所示，将远程路径设置为`/home/mist`。
> 如果需要同时部署多个项目，建议提前在服务器上新建文件夹，然后将远程路径设置到`/home/mist/<文件夹名>`

{% asset_img pyc8.png %}

{% asset_img pyc9.png %}

完成后点击下方的创建按钮即可。

# 配置SSH解释器(2022.1-)

打开项目后，进入Pycharm设置，选择`项目-Python解释器`，点击右上角的齿轮按钮并选择`添加`

{% asset_img pyc31.png %}

## 设置服务器信息

选择`SSH解释器`并依次填入服务器域名、SSH端口。用户名固定为`mist`

{% asset_img pyc32.png %}

- 如果没有私钥，则将创建服务器时设置的服务器密码填入密码框中并下一步
- 如果有私钥，则点击`密钥对`按钮，点击红框出的文件夹图标选择`.pem`私钥文件后下一步

{% asset_img pyc33.png %}

## 设置解释器路径

点击解释器一栏右侧的文件夹图标，找到解释器路径

{% asset_img pyc34.png %}

- 如果使用默认环境，则找到`/usr/local/bin/python`即可
- 如果使用conda虚拟环境，则需要找到**激活环境**后`which python`返回的路径，如下图所示

{% asset_img pyc7.png %}

## 设置同步文件夹

按下图所示，将远程路径设置为`/home/mist`。
> 如果需要同时部署多个项目，建议提前在服务器上新建文件夹，然后将远程路径设置到`/home/mist/<文件夹名>`

{% asset_img pyc35.png %}

{% asset_img pyc36.png %}

设置好后点击下方的完成按钮即可。

{% asset_img pyc37.png %}

# 完成

{% asset_img pyc10.png %}

完成后Pycharm将开始上传文件并更新解释器索引。上传耗时取决于您的网络上行带宽；更新索引一般需要几分钟。

Pycharm默认会重复上传并覆盖服务器里已有的文件，可以到菜单栏`工具-部署`中点击选项修改。

{% asset_img pyc17.png %}

**取消选择**覆盖最新文件，选上创建空目录即可。

{% asset_img pyc18.png %}

***

完成后在Pycharm界面右下角，能看到红框1处所示当前的解释器已变为`Remote Python`，以及红框2处所示的部署服务器。

{% asset_img pyc11.png %}

若需要换回本地环境运行，则分别点这两个地方，将解释器设置为本地的解释器，部署设置为`无默认服务器`

# 运行

当右下角解释器为`Remote Python`时，点击运行/调试按钮即可使用服务器的算力执行程序

## 编辑配置

在Pycharm界面右上角点击编辑配置，可以修改程序运行时需要的参数及环境变量
{% asset_img pyc19.png %}

### 设置运行参数

部分程序要求在终端中传入对应的参数，可在编辑配置页面的`形参`中设置对应地参数。

{% asset_img pyc20.png %}

如原本命令为`python train.py -net resnet152 -gpu -b 120`，那么就在形参中写`-net resnet152 -gpu -b 120`

### 设置环境变量

如果需要修改环境变量，则点击环境变量右边的小图标

{% asset_img pyc22.png %}

将需要添加的环境变量以键值对的形式添加进去即可

{% asset_img pyc23.png %}

# 启动服务器终端

在菜单栏`工具-部署`中点击`启动SSH会话`即可打开服务器的终端

{% asset_img pyc27.png %}

> 直接点击`Terminal`默认启动的是自己电脑的终端，注意不要混淆了

{% asset_img pyc28.png %}

# 浏览/下载服务器中的文件

在菜单栏`工具-部署`中点击`浏览远程主机`即可查看到服务器上的文件

{% asset_img pyc24.png %}

进入`/home/mist/`文件夹后，右键点击文件即可下载到本地或执行其他操作

{% asset_img pyc25.png %}

# 排查

如果在使用pycharm过程中遇到了问题，则可以用下面的方法排查。

进入Pycharm设置，按下图所示点击选择全部显示

{% asset_img pyc12.png %}

## 修改服务器端口/解释器路径(2022.2+)

1. 删除已有的解释器，点击加号并选择SSH
2. 在SSH连接中选择现有，并点击下图2所示的右侧的三个点

{% asset_img pyc14.png %}

3. 选择要修改的配置，设置好新端口后点测试连接。连接成功后确认，点击下一步。

{% asset_img pyc15.png %}

4. 选择系统解释器，点击解释器右侧的三个点，定位到新的地址后确认。
5. 同步文件夹同上，设置到`/home/mist`下即可

{% asset_img pyc16.png %}

6. 完成