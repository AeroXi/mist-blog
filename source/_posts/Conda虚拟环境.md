---
title: conda创建虚拟环境
date: 2021-02-03 14:00:00
tags: miniconda
---
每台服务器创建时均已配好miniconda3的环境

# 找不到conda命令
如在终端中输入`conda`后提示`conda: command not found`,
则需要手动配置一下环境变量：`export PATH=$PATH:/mistgpu/miniconda3`
**旧镜像conda目录为`/home/mist/miniconda3/`，新镜像为`/mistgpu/miniconda3/`*

# 创建虚拟环境
在终端中输入`conda create -n 环境名`即可，环境名可任意取
也可以在创建的时候指定所需要的包，建议用`conda create -n 环境名 python=3.6`创建。
*推荐创建时一并安装所有需要的包，这样conda可以自行匹配互相兼容的版本。*

{% asset_img 1.png %}

输入`y`开始创建。

# 激活环境
创建完成后的环境需要激活才可生效，使用`conda activate 环境名`即可激活。
激活后在终端提示符最左边会出现`(环境名)`，表示激活成功。同时可以用下面的两条命令检查是否使用的是虚拟环境里的程序。
- `python -V`
- `pip -V`
**注: 为防止pip安装时升级/降级其他已装的包导致破坏环境依赖，建议在conda创建的环境内使用`conda install 包名`来安装所需的包。*
{% asset_img 2.png %}

# 在Jupyter中使用conda创建的环境
默认情况下，服务器附加功能里的Jupyter使用的是conda以外的环境。
要想在Jupyter中使用创建后的环境需要如下配置：
1. 使用`conda activate 环境名`激活环境
2. 在虚拟环境内输入: `conda install ipykernel`
3. 将ipykernel安装到默认环境中(不需要退出虚拟环境): 
`python -m ipykernel install --user --name mistvenv --display-name "虚拟环境"`
(此命令中`--name`后的名称要和之前的环境名一致，`--display-name`后的名称可自定义)
{% asset_img 3.png %}
4. 重新打开Jupyter，完成。
{% asset_img 4.png %}

已有的ipynb文件也可以通过右上角切换环境
{% asset_img 6.png %}
{% asset_img 5.png %}

# 在PyCharm中使用conda创建的环境
PyCharm具体配置教程可参考[http://blog.mistgpu.com/2021/02/01/PyCharm连接教程/#添加SSH解释器)](http://blog.mistgpu.com/2021/02/01/PyCharm%E8%BF%9E%E6%8E%A5%E6%95%99%E7%A8%8B/#%E6%B7%BB%E5%8A%A0SSH%E8%A7%A3%E9%87%8A%E5%99%A8)
1. 使用`conda activate 环境名`激活环境
2. 在虚拟环境内输入: `which python`

{% asset_img 5-1.png %}

3. 将返回的路径名(上图红框)填入SSH解释器中在`解释器`一栏(蓝框)

{% asset_img 5-2.png %}

# 降级cuda版本
在conda中可以通过安装`cudatoolkit`来降级cuda版本。

{% asset_img 8.png %}

通过`conda search cudatoolkit`可以看到可安装的版本，安装使用`conda install cudatoolkit=版本号`。
**推荐一条命令内安装好所有需要的包**，如`conda install tensorflow-gpu=1.13.1 cudatoolkit keras ......`。

本例安装cuda9.2，`conda install cudatoolkit=9.2`
在虚拟环境里还需要装需要用到的包，使用[PyTorch官方](https://pytorch.org/get-started/previous-versions/)的代码安装后测试成功。
{% asset_img 9.png %}
# conda下载慢 / CondaHTTPError
{% asset_img 7.png %}
出现这种情况时可以重试几次，如果一直失败请使用pip下载。