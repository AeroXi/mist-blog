---
title: VSCode连接教程
date: 2020-04-08 17:45:55
tags:
---

VSCODE连接云服务器教程

首先，在vscode商店内安装Remote-SSH与Remote-SSH:EDITING 插件
{% asset_img 5fbd279d2b88fd29ffd414af6c3aa6f6.png %}

切换至ssh标签页，点击加号

{% asset_img a3475195868f80a64a64ef3a2351243d.png %}

随后，在弹出的框中完整复制服务器管理页面的ssh命令

{% asset_img 734d301fee875704909d72f6510ba03a.png %}


选择您windows系统用户下的config文件夹，图中为第一个（此处电脑用户名为benak）

{% asset_img dbf153714151fae168aca6b3c5b76273.png %}


随后，输入创建服务器时您输入的密码

稍后就可以直接开始使用。

{% asset_img 8f09ae13a8d1dc6daa400530b26f0976.png %}


点击右侧的+窗口按钮，即可在新窗口中连接至服务器。

不过每次进入新的文件夹均需要重新输入密码，有些许麻烦。以下的内容为启用公钥连接，这样连接时就不需要输入密码。

以管理员权限打开cmd，输入ssh-keygen -t rsa 

然后应该会在.ssh文件下见到生成的公钥密钥

{% asset_img bd11f6fd7207322e15f419b0cfa13846.png %}


将id_rsa.pub文件上传至服务器

进入SSH配置目录，

cd \~/.ssh

ls

查看一下是否有一个名为authorized_keys的文件，如果没有就创建一个，然后把刚上传的id_rsa.pub中的内容附到authorized_keys文件中，

touch authorized_keys

cat \~/id_rsa.pub \>\> authorized_keys

随后，更改权限，确保公钥生效

chmod -R 600 authorized_keys

最后点击远程连接界面中的齿轮，打开配置文件（与上文提及的相同）

{% asset_img 510134d5e3bc7bf9eb7c884215da3ba4.png %}


{% asset_img 55c1bdcbc84cfd38e9be60a1c6d34fcb.png %}


在config最后加入PasswordAuthentication no并保存，即可登录。

Host名可随意更改，避免冲突。
