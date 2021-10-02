---
title: conda创建虚拟环境
date: 2021-02-03 14:00:00
tags: miniconda
---
每台服务器创建时均已配好miniconda3的环境

# 找不到conda命令
如在终端中输入`conda`后提示`conda: command not found`,
则需要手动配置一下环境变量：`export PATH=$PATH:/mistgpu/miniconda3/bin`

# 创建虚拟环境
在终端中输入`conda create -n 环境名`即可，环境名可任取。也可以在创建的时候指定所需要的包及对应版本(推荐)，

如`conda create -n 环境名 python=3.8 ipykernel pandas matplotlib ... -y`。

之后等待conda下载完即可，下载完成时会有下图提示：

{% asset_img conda1.png %}

# 激活环境
创建完成后的环境需要激活才可生效，使用`conda activate 环境名`即可激活。激活成功后在终端提示符上边会出现`(环境名)`。
同时可以用以下命令检查python版本及路径(路径应当在`Miniconda`目录中，而不是默认的`/usr/bin`)。
- `python -V`
- `which python`

{% asset_img conda2.png %}


# 安装其他的包
虚拟环境创建后不会继承默认环境里的包，意味着程序所需的包都需要在虚拟环境中**重新安装**。

若在创建时没有一次性装完，可以继续在终端中输入`conda install 包名 -y`安装剩余的包

注：为了确保不同包的版本之间能互相兼容，在conda环境中请尽量在一条命令内安装好所有的包，并尽量不要使用pip安装。

# 在Jupyter中使用conda创建的环境
默认情况下，服务器附加功能里的Jupyter使用的是默认的pip环境。 若要想在Jupyter中使用conda创建的虚拟环境，需要如下配置：
1. 使用`conda activate 环境名`激活环境
2. 在虚拟环境内输入: `conda install ipykernel ipython_genutils -y`
3. 将ipykernel安装到默认环境中(不需要退出虚拟环境): 
`python -m ipykernel install --user --name mistvenv --display-name "虚拟环境"`
(此命令中`--name`后的名称要和之前的环境名一致，`--display-name`后的名称可自定义)

{% asset_img conda3.png %}

4. 重新打开Jupyter，点击左上角蓝色+号新建启动器即可看到虚拟环境了。
{% asset_img conda4.png %}

已有的ipynb文件可以通过点击右上角的python切换环境。
{% asset_img conda5.png %}

# 在PyCharm中使用conda创建的环境
PyCharm具体配置教程可参考[http://blog.mistgpu.com/2021/02/01/PyCharm连接教程/#添加SSH解释器)](http://blog.mistgpu.com/2021/02/01/PyCharm%E8%BF%9E%E6%8E%A5%E6%95%99%E7%A8%8B/#%E6%B7%BB%E5%8A%A0SSH%E8%A7%A3%E9%87%8A%E5%99%A8)
1. 使用`conda activate 环境名`激活环境
2. 在虚拟环境内输入: `which python`，复制返回的路径名。

{% asset_img conda6.png %}

3. 将返回的路径名(上图红框)填入SSH解释器中在`解释器`一栏(蓝框)

{% asset_img conda7.png %}

# 降级cuda版本
在conda中可以通过安装`cudatoolkit`来切换cuda版本。
注：**RTX30系、A5000、A6000、A100等安培架构机型不支持降级到cuda11以下。**

通过`conda search cudatoolkit`可以看到可安装的版本，使用`conda install cudatoolkit=版本号 -y`安装。

{% asset_img conda8.png %}

虚拟环境内安装的`cudatoolkit`的版本就对应了`cuda`的版本，使用`conda list`确认此包已安装即可使用。
- *使用`nvidia-smi`命令查询的cuda版本为驱动最高支持的cuda版本，不代表环境的cuda版本。*
- *使用`nvcc -V`命令查询到的cuda版本为默认pip环境的cuda版本，不是虚拟环境内的版本。*

# 例：安装旧版本PyTorch

在[PyTorch官方网站](https://pytorch.org/get-started/previous-versions/)找到对应PyTorch版本-Linux-conda部分的命令，并选择所需`CUDA`版本。
{% asset_img conda9.png %}
本例以安装1.7.1版本的PyTorch，10.2版本的cuda为例。

激活环境后粘贴命令即可。需要下载的包比较大，请耐心等待。

{% asset_img conda10.png %}

安装完成后确认PyTorch版本为`1.7.1`，cuda版本为`10.2`，cudnn版本为`7.6.5`，GPU可用。

{% asset_img conda11.png %}

# 常见问题
## 环境冲突(Found Conflicts)
遇到冲突时一般会有类似下图的提示，若环境内装了很多包的话会卡在红框处。此时可以`Ctrl-c`直接取消，也可在等待完成后查看具体哪些包直接有冲突。
{% asset_img conda12.png %}
解决方案包括但不限于：
- 重新创建虚拟环境，并将所有要用到的包放在一条命令内安装
- 放宽各个包版本要求

## 使用自定义源时404或403报错
为了加快conda的下载速度，我们在环境中修改了默认镜像源。这可能导致使用其他自定义源时报错。
{% asset_img conda13.png %}
您可以在终端中使用`rm ~/.condarc`命令删除自定义配置后重试。
{% asset_img conda14.png %}
*删除`.condarc`后将使用默认源下载包，速度会比使用镜像更慢。*