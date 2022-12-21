---
title: SSH连接教程
date: 2022-11-25 12:00:00
tags:
---
通过SSH连接可以进入到服务器执行各种操作，将会涉及到Linux命令，如不熟悉Linux命令请谨慎操作。

## 重要提示
SSH连接遇到网络波动时会中断，前台运行的进程**会被终止**。

如果程序没有挂到后台或代码没有保存断点的话，您的程序很有可能因此白跑。

因此如果需要长时间运行程序，请务必使用nohup或screen挂到后台运行，并建议在代码中设置保存断点。

方法一：运行命令改为 `nohup 原命令 &`，输出在`nohup.out`文件中
方法二：(推荐!) 在运行程序前 先在终端中输入 `screen -SL 会话名 -Logfile 日志名` 新建会话

> 会话名与日志名自定。
> 需要在运行程序前启动screen，开始运行后无法操作

之后输入需要执行的命令(如`python 文件名.py`)。
输入 `screen -dr 会话名` 恢复会话；程序输出可恢复会话或查看日志文件

具体screen使用教程请参考[终端使用教程](http://blog.mistgpu.com/2022/11/21/%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%BB%88%E7%AB%AF%E4%BD%BF%E7%94%A8%E6%95%99%E7%A8%8B/#screen%E4%BD%BF%E7%94%A8%E6%8C%87%E5%8D%97)

## 本机终端 
> Win10+, macOS, Linux 可用

### 下载私钥文件`用户名.pem`并放在用户目录下

* Windows: `C:\Users\<账户名>\<用户名>.pem`
* macOS: `/Users/<账户名>/<用户名>.pem`
* Linux: `/home/<账户名>/<用户名>.pem`

### 启动终端

* Windows: 在开始菜单中搜索`cmd`或`powershell`
* macOS: 按下`Command + 空格`，在Spotlight中搜索`终端`
* Linux: Ubuntu系统可用`Ctrl + alt + t`快捷键启动

### 在打开的终端窗口中粘贴SSH命令

```commandline
ssh -i ~/<用户名>.pem mist@<服务器域名> -p <ssh端口>
```

初次连接机器时会询问是否接受服务器指纹，会有下图红框的提示。输入`yes`即可。

{% asset_img ssh-1.png %}

如果没有私钥文件，则会提示输入密码，如下图所示。

{% asset_img ssh-2.png %}

此时需要输入创建服务器时设置的服务器密码，输入过程中字符**不会显示在屏幕上**，输入完成后回车即可。

### 确认已连接

成功连接上机器后会显示MistGPU及注意事项，同时终端标识符会变成如下图红框处所示。

{% asset_img ssh-3.png %}

其中红色的`$`字符表示可以在此处输入命令。

## Termius
> Win7+, macOS, Linux 可用

从[Termius官网](https://termius.com/download/)下载后安装，打开后在`Host`边栏中依次选择`Add` - `New Host`

{% asset_img termius1.png %}

### 填写服务器信息

在右侧边栏中一次填入以下信息

- Label: 连接名称，任取，可选
- Address: 服务器域名，必填
- Port: SSH端口，必填
- Username: 用户名，固定为mist

- 如果没有私钥，则将创建服务器时设置的服务器密码填入Password中
- 如果有私钥，则点击粉框6处的`Set a Key`按钮

{% asset_img termius2.gif %}

### 连接到服务器

配置完成后双击连接即可。初次连接服务器时会提示是否添加指纹，选择`Add & continue`即可。

{% asset_img termius3.gif %}

## PuTTY
> Win7+ 可用

### 安装PuTTY

- [PuTTY官网](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)
- [清华镜像站](https://mirrors.tuna.tsinghua.edu.cn/putty/latest.html)

{% asset_img putty1.png %}

### 填写服务器信息

在红框1处分别填入`mist@服务器域名`以及`SSH端口`

- 如果没有私钥，则点击右下角的`Open`按钮连接即可
- 如果有私钥，则进入粉框2处选择私钥文件`用户名.ppk`，如下图所示
> PuTTY及WinSCP不支持`.pem`文件，请使用`.ppk`文件

{% asset_img putty2.png %}

选择好文件后点击右下角`Open`按钮连接。

初次连接服务器时会有下图提示，选择`Accept`即可

{% asset_img putty3.png %}

### 完成

同上，连接成功后会有欢迎语以及注意事项，看到红色`$`符号后输入命令即可。

{% asset_img putty4.png %}

## Xshell
> Win7+ 可用

### 安装Xshell

在[Xshell官网](https://www.xshell.com/zh/free-for-home-school/)下载并安装Xshell，下载链接会发送到个人邮箱中。

### 新建配置

点击左上角`文件`菜单栏中选择`新建`

{% asset_img xshell1.png %}

- 名称：连接名称，任取
- 协议：SSH
- 主机：服务器域名(不包括`mist@`)
- 端口号：SSH端口

### 设置用户名及密码/私钥

点击红框1处的`用户身份验证`，右侧用户名固定为`mist`

- 如果没有私钥，则在红框2中只勾选`Password`，并在上方填入创建服务器时设置的服务器密码
- 如果有私钥，则在红框2中只勾选`Public Key`，并在选中此项的情况下点击红框3中的`设置`

{% asset_img xshell2.png %}

在弹出的Public key设置窗口中依次点击`浏览`，`导入`。选择`.pem`私钥文件确认即可

{% asset_img xshell3.gif %}

### 连接机器

初次连接服务器时会有下图提示，选择`接受并保存`即可

{% asset_img xshell4.png %}