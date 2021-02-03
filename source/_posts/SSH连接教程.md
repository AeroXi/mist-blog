---
title: SSH连接教程
date: 2021-02-03 18:00:00
tags: ssh
---
# 概述
通过SSH连接可以进入到服务器执行各种操作，将会涉及到Linux命令，如不熟悉Linux命令请谨慎操作。

{% asset_img 0.png %}
在开始前请参考[常见问题](https://www.mistgpu.com/faq/)。
短时间执行的命令可以直接执行，但需要长时间的任务请务必使用`screen`或其他方法挂到后台运行。
# 网页终端
## Jupyter
在服务器开机的状态下点击附加功能中的Jupyter即可进入。在Launcher启动页点Terminal即可。
{% asset_img 1.png %}
{% asset_img 2.png %}
Launcher可点击左上角篮筐中的加号启动。
## 网页命令行
点击附加功能的命令行即可。
# 本地终端
## 通用步骤
在[控制台](https://www.mistgpu.com/user/)可以复制SSH命令，直接粘贴到命令行中即可连接。
{% asset_img 3.png %}
{% asset_img 4.png %}
上图中蓝色部分为输入的内容，从上到下依次为：
- 粘贴ssh命令
- 第一次连接需要接收服务器指纹，输入`yes`即可
- 输入密码，密码为**创建服务器**时设置的，输入过程中不会显示在屏幕上，输完回车即可
出现类似红色框中的提示则表示连接成功。(带有MistGPU字样)
## Windows 10系统
Win10系统已自带`ssh`，`scp`等命令，在命令行或`Powershell`中都可直接使用。
## macOS
按下`Command + 空格键`，在Spotlight中输入`终端`即可打开终端。
## Linux
在应用程序中找到终端即可。Ubuntu系统可用`Ctrl - alt - t`快捷键启动。
## Win10以下或SSH命令不可用
**以下几种方法的主机名(Host)和端口均可在服务器的`附加功能-使用帮助`中看到。**
### PuTTY
从[PuTTY官网](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)下载PuTTY安装即可，可选择msi安装包一键安装，也可只下载PuTTY程序本身直接运行。
{% asset_img 5.png %}

打开程序后填入`主机名`和`SSH端口`即可。

{% asset_img 6.png %}

本例中在`主机名`中填入`mist@gpu193.mistgpu.xyz`，`端口`中填入`20500`。请以实际为准。
完成后点击Open即可连接了。同理第一次连接时要点`Yes`按钮，之后输入**创建服务器时**设置的密码。
### MobaXterm
从[MobaXterm官网](https://mobaxterm.mobatek.net/download-home-edition.html)下载安装即可。在下载页左边蓝色的Portable为便携版，可直接双击运行，右边绿色的Installer为安装版。
#### 方法一：
设置本地的终端为MobaXterm自带的Bash，然后在主页新建本地终端，粘贴ssh命令即可。
{% asset_img 7.png %}
{% asset_img 7-1.png %}
#### 方法二：
新建SSH会话，填入主机名和ssh端口后即可连接。
{% asset_img 8.png %}
### XShell
该[下载链接](https://www.netsarang.com/zh/free-for-home-school/)获取该软件的家庭和学校用户免费版本（建议在获取下载链接的时候选中“两者”，即下载Xshell和Xftp，前者是操作服务器的命令行窗口，后者是专门用于文件传输的），后安装打开。
{% asset_img xs0.png %}
点击如上图所示的图标来新建会话，在弹出来的设定窗口中，名称可任意填写，协议选择SSH。

{% asset_img xs1.png %}
填充完如上图所示，然后点击下方的“连接”完成设定并主动尝试连接。

{% asset_img xs2.png %}
完成后软件左侧会出现刚创建的会话，在弹出来的窗口（如上图所示）中填入用户名mist，并勾选“记住用户名”，点击“确定”登录。

{% asset_img xs3.png %}
在接下来的窗口（如上图所示）中输入创建服务器时的密码，并勾选“记住密码”后点击确定可成功连接。
