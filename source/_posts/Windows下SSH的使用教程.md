---
title: Windows下SSH的使用教程
date: 2020-04-08 15:00:00
tags:
---
## 概述
本文将主要介绍Windows平台下各种SSH连接上服务器的方法，如果您只是想在服务器中进行命令操作，建议结合您的使用习惯，使用我们提供的附加功能（如下图所示），可以直接连接上服务器操作。
{% asset_img cmd0.PNG %}
下面将介绍几种SSH连接方式:

## 命令行
###启动命令行
{% asset_img cmd1.PNG %}
按住如图所示的徽标键，同时按下键盘上的R，在弹出的运行命令框中输入cmd，按下回车后便能启动命令行。

###运行SSH
{% asset_img cmd2.PNG %}
点开[服务器管理](https://mistgpu.com/user/)，复制如上图所示的命令，并粘贴在刚才打开的命令行窗口，然后回车。（P.S. 如果没有SSH服务，请参照[这里](https://jingyan.baidu.com/article/9158e0002c159ea254122821.html)进行配置）

{% asset_img cmd3.PNG %}
第一次连接将会出现如上图所示提示，输入yes，然后回车，接下来输入您在**创建服务器时输入的密码**便可实现SSH连接上服务器。

##WSL
WSL，全称是Windows Subsystem for Linux，即适用于Linux的Windows子系统，相比于命令行的好处就是可以使用Linux的相关命令，字体渲染也比较美观，请参照[这里](https://jingyan.baidu.com/article/e4d08ffd5849e20fd2f60d93.html)进行WSL的安装。
安装成功后可以通过快捷方式打开或者启动命令行输入wsl打开，打开以后的ssh连接操作同命令行运行SSH的方法，复制粘贴[服务器管理](https://mistgpu.com/user/)中的命令，回车运行，输入密码进行连接。

## MobaXterm
在该[下载链接](https://mobaxterm.mobatek.net/download.html)获取该软件后安装打开。
{% asset_img mx0.PNG %}
点击如上图所示的图标来新建会话，在弹出来的设定窗口中选择上方的SSH，在Basic SSH settings进行服务器信息配置。

{% asset_img mx1.PNG %}
以ssh mist@gpu28.mistgpu.xyz -p 40000为例，Remote host应填入gpu28.mistgpu.xyz，即服务器主机地址（一般在@后）；选中Specify username，填入mist，即用户名（一般在@前）；最后将Port中的数字改成40000，即端口号（一般为-p后的数字），填充完如上图所示，然后点击下方的OK完成设定。完成后软件会试图连接，需要输入密码，输入在创建服务器时的密码后按下回车便能成功连接。

## Xshell
在该[下载链接](https://www.netsarang.com/zh/free-for-home-school/)获取该软件的家庭和学校用户免费版本（建议在获取下载链接的时候选中“两者”，即下载Xshell和Xftp，前者是操作服务器的命令行窗口，后者是专门用于文件传输的），后安装打开。
{% asset_img xs0.PNG %}
点击如上图所示的图标来新建会话，在弹出来的设定窗口中，名称可任意填写，协议选择SSH。以ssh mist@gpu28.mistgpu.xyz -p 40000为例，主机应填入gpu28.mistgpu.xyz，端口号中的数字改为40000。

{% asset_img xs1.PNG %}
填充完如上图所示，然后点击下方的“连接”完成设定并主动尝试连接。

{% asset_img xs2.PNG %}
完成后软件左侧会出现刚创建的会话，在弹出来的窗口（如上图所示）中填入用户名mist，并勾选“记住用户名”，点击“确定”登录。

{% asset_img xs3.PNG %}
在接下来的窗口（如上图所示）中输入创建服务器时的密码，并勾选“记住密码”后点击确定可成功连接。
