---
title: SSH连接教程
date: 2021-02-03 18:00:00
tags: ssh
---

# 概述

通过SSH连接可以进入到服务器执行各种操作，将会涉及到Linux命令，如不熟悉Linux命令请谨慎操作。

{% asset_img ssh0.png %}

在开始前请参考[常见问题](https://www.mistgpu.com/faq/)。
需要长时间运行的任务请**务必**使用`screen`或其他方法挂到后台运行。

# 网页终端

## Jupyter

在服务器开机的状态下可直接点击`进入环境`打开Jupyter。

{% asset_img ssh1.png %}

点击`文件 - 新建 - 终端`或直接在启动页点击`终端`即可。

> 注意是黑色的终端`Terminal`而不是蓝色的控制台`Console`。

{% asset_img jupyter1.png %}

Launcher可点击左上角篮筐中的加号启动。

## 网页命令行

点击附加功能的命令行即可。

{% asset_img ssh2.png %}

# 本地终端

## Win10/Win11, macOS, Linux

在[控制台](https://www.mistgpu.com/user/)复制SSH命令，直接粘贴到命令行中即可连接。

{% asset_img ssh4.png %}

上图中蓝色部分为输入的内容，从上到下依次为：

- 粘贴ssh命令
- 第一次连接需要接收服务器指纹，输入`yes`即可
- 输入密码，密码为**创建服务器**时设置的，输入过程中**不会显示**在屏幕上，输完回车即可

看到`mist @ MistGPU`的提示即表示连接成功

{% asset_img ssh5.png %}

## Win10/Win11

在开始菜单中搜索`cmd`或`powershell`

{% asset_img cmd.png %}
{% asset_img powershell.png %}

## macOS

按下`Command + 空格键`，在Spotlight中输入`终端`即可打开终端。

## Linux

在应用程序中找到终端即可。Ubuntu系统可用`Ctrl-alt-t`快捷键启动。

---

## Win10以下或SSH命令不可用

> 以下几种方法的主机名(Host)和端口均可在服务器的 `附加功能-使用帮助` 中查询。

### PuTTY

从[PuTTY官网](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)下载PuTTY安装即可，可选择msi安装包一键安装，也可只下载PuTTY程序本身直接运行。
{% asset_img putty0.png %}

打开程序后填入`主机名`和`SSH端口`即可。

{% asset_img putty1.png %}

本例中在`主机名`中填入`gpu294.mistgpu.com`，`端口`中填入`12601`。请以实际为准。

完成后点击Open即可连接了。同理第一次连接时要点`Accept`接受指纹。

{% asset_img putty2.png %}

之后分别输入用户名`mist`以及**创建服务器时**设置的密码。

> 输入密码过程中 输入的字符**不会显示**在屏幕上，输完回车即可
 
{% asset_img putty3.png %}

### MobaXterm

从[MobaXterm官网](https://mobaxterm.mobatek.net/download-home-edition.html)
下载安装即可。在下载页左边蓝色的Portable为便携版，可直接双击运行，右边绿色的Installer为安装版。

#### 方法一：

打开软件后点击`Start local termial`，然后直接粘贴ssh命令即可

{% asset_img moba1.png %}

#### 方法二：

点击 `Session - SSH` ，填入`IP`和`端口`即可。

### XShell

该[下载链接](https://www.netsarang.com/zh/free-for-home-school/)
获取该软件的家庭和学校用户免费版本（建议在获取下载链接的时候选中“两者”，即下载Xshell和Xftp，前者是操作服务器的命令行窗口，后者是专门用于文件传输的），后安装打开。
{% asset_img xs0.png %}
点击如上图所示的图标来新建会话，在弹出来的设定窗口中，名称可任意填写，协议选择SSH。

{% asset_img xs1.png %}
填充完如上图所示，然后点击下方的“连接”完成设定并主动尝试连接。

{% asset_img xs2.png %}
完成后软件左侧会出现刚创建的会话，在弹出来的窗口（如上图所示）中填入用户名mist，并勾选“记住用户名”，点击“确定”登录。

{% asset_img xs3.png %}
在接下来的窗口（如上图所示）中输入创建服务器时的密码，并勾选“记住密码”后点击确定可成功连接。

---

# 常用操作

连接好进入命令行终端后便可开始操作了，常用的操作命令包括

- `ls -l` 查看当前目录下的文件; `ls -l /data` 查看云存储中的文件
- `cd 目录名` 进入到指定目录; `cd ../` 返回到上一级目录; `cd ~/`返回到主目录
- `pwd` 查看当前目录的绝对路径
- `cp 文件 目录` 将`文件`复制到`目录`中; `mv 文件 目录`将`文件`移动到`目录`中
- `python3 文件名.py` 运行指定的python程序
- `pip install 包名 --user` 使用`pip`安装模块
- `nvidia-smi` 查看当前显卡使用情况，可用`py3smi`代替
- `unzip 要解压的文件名.zip -d 解压后的目录名` 将该`文件`解压到指定`目录`下
- `zip -r9 保存后文件名.zip 要压缩的目录名` 将`目录`下的所有文件压缩成`文件`

# 注意事项

- 所有命令均需要以英文半角状态输入，请特别留意不要漏掉命令中的空格，否则会报错。
- 长时间运行的任务请务必挂到后台运行，详情请见[常见问题](https://mistgpu.com/faq)