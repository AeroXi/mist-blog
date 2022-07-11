---
title: conda创建虚拟环境
date: 2021-02-03 14:00:00
tags: miniconda
---

# 前言

本教程中使用的`mamba`命令在cuda11.6及更新版镜像中可用，旧版镜像请手动替换为`conda`
> `mamba`是`conda`的C++实现，速度更快。常用语法与`conda`并无区别

# 创建虚拟环境

在终端中输入`mamba create -n 环境名 -y`即可，环境名可任取。

推荐在创建虚拟环境是顺带指定需要的python版本，

如`mamba create -n 环境名 python=3.8 -y`。

之后等待下载即可，下载完成时会有下图提示：

{% asset_img conda1.png %}

# 激活环境

创建完成后的环境需要激活才可生效，使用`mamba activate 环境名`即可。激活成功后在终端提示符上边会出现`(环境名)`的提示。
同时可以用以下命令检查python版本及路径(路径应当在`miniconda`目录中，而不是自带的`/usr/local/bin`)。

- `python -V`
- `which python`

{% asset_img conda2.png %}

# 安装其他的包

虚拟环境创建后不会继承默认环境里的包，意味着程序所需的包都需要在虚拟环境中**重新安装**。

继续在终端中输入`mamba install 包名 -y`安装即可
> 为确保包之间的兼容性，推荐用`mamba`而不是`pip`来安装

# 在Jupyter环境中使用虚拟环境

1. 使用`mamba activate 环境名`激活环境
2. 在虚拟环境内输入: `mamba install ipykernel ipython_genutils -y`
3. 执行 `python -m ipykernel install --user --name 虚拟环境名 --display-name "显示名称"`

> 此命令中`--name`后的名称要和之前的环境名一致，`--display-name`后的名称可任取。

{% asset_img conda3.png %}

4. 刷新Jupyter网页，之后点击左上角蓝色+号新建启动器即可看到虚拟环境了。

   {% asset_img conda4.png %}

已有的ipynb文件可以点击右上角或`菜单栏-内核-更改内核`修改。

{% asset_img conda5.png %}

# 在PyCharm中使用conda创建的环境

PyCharm具体配置教程可参考[http://blog.mistgpu.com/2021/02/01/PyCharm连接教程/#添加SSH解释器)](http://blog.mistgpu.com/2021/02/01/PyCharm%E8%BF%9E%E6%8E%A5%E6%95%99%E7%A8%8B/#%E6%B7%BB%E5%8A%A0SSH%E8%A7%A3%E9%87%8A%E5%99%A8)

1. 使用`mamba activate 环境名`激活环境
2. 在虚拟环境内输入: `which python`，复制返回的路径。

{% asset_img conda6.png %}

3. 将返回的路径填入SSH解释器中在`解释器`一栏(下图蓝框)

{% asset_img img.png %}

# 降级cuda版本

在虚拟环境中可以通过安装不同版本的`cudatoolkit`来切换环境内的cuda版本。

注：**RTX30系、A5000、A6000、A100等安培架构机型不支持降级到cuda11以下。**

通过`mamba search cudatoolkit`可以看到可安装的版本。使用`mamba install cudatoolkit=版本号 -y`即可安装。

> 如果需要安装PyTorch或TensorFlow可跟随后面的教程一并安装，不需要现在装

{% asset_img conda8.png %}

虚拟环境内安装的`cudatoolkit`的版本就对应了`cuda`的版本，激活环境后输入`mamba list`确认此包已安装即可使用。

{% asset_img cuda1.png %}

- *使用`nvidia-smi`命令查询的cuda版本为驱动最高支持的cuda版本，不代表环境的cuda版本。*
- *使用`nvcc -V`命令查询到的cuda版本为默认pip环境的cuda版本，不是虚拟环境内的版本。*

# 例：安装旧版本PyTorch

在[PyTorch官方网站](https://pytorch.org/get-started/previous-versions/)找到对应PyTorch版本-Linux-conda部分的命令，并选择所需`CUDA`版本。

教程以安装`PyTorch11.1`, `cuda=11.3`为例：

{% asset_img conda9.png %}

激活环境后 (*可选, 将命令开头的`conda`替换成`mamba`*) 粘贴命令执行即可。

> 如果不需要`torchvision`和`torchaudio`可以从命令中去掉。

> 此步骤需要下载的包比较大，请耐心等待。

{% asset_img conda10.png %}

安装完成后可确认PyTorch版本为`1.11.0`，GPU可用，cuda版本为`11.3`，cudnn版本为`8.2.0`。

{% asset_img conda11.png %}

# 例：安装旧版本TensorFlow

在[TensorFlow官网](https://www.tensorflow.org/install/source#gpu)确认需要安装的版本所需的`cuDNN`及`CUDA`版本

教程以安装`tensorflow=2.6.0`为例：

{% asset_img conda12.png %}

激活环境后执行 `mamba install -c conda-forge cudatoolkit={CUDA版本} cudnn={cuDNN版本} -y`

{% asset_img conda13.png %}

粘贴执行下面两条命令

```shell
mkdir -p $CONDA_PREFIX/etc/conda/activate.d
echo 'export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$CONDA_PREFIX/lib/' > $CONDA_PREFIX/etc/conda/activate.d/env_vars.sh
```

{% asset_img conda14.png %}

通过pip安装TensorFlow

`pip install --upgrade pip`

`pip install tensorflow=={tf版本}`

{% asset_img conda15.png %}

安装完成后可确认TensorFlow版本为`2.6.0`，GPU可用

{% asset_img conda16.png %}

# 常见问题

## 找不到`conda`: `command not found`

在终端中手动执行 `export PATH=$PATH:/mistgpu/miniconda/bin`，之后执行`conda init --all`后重启终端

## 环境冲突(Found Conflicts)

遇到冲突时一般会有类似下图的提示，若环境内装了很多包的话会卡在红框处。

此时可以`Ctrl-c`直接取消，也可在等待完成后查看具体哪些包直接有冲突。

{% asset_img conda17.png %}

解决方案包括但不限于：

- 重新创建虚拟环境，并将所有要用到的包放在一条命令内安装
- 放宽各个包版本要求

## 使用自定义源时404或403报错

为了加快conda的下载速度，我们在环境中修改了默认镜像源。这可能导致使用其他自定义源时报错。

{% asset_img conda18.png %}

您可以在终端中使用`rm ~/.condarc`命令删除自定义配置后重试。

{% asset_img conda19.png %}

*删除`.condarc`后将使用默认源下载包，速度会比使用镜像更慢。*

# 降级默认环境的cuda(不推荐)

> 一般情况下不需要使用，如果虚拟环境里降级有问题必须降默认环境的cuda才考虑

> 搞砸了的话需要重新创建服务器

到[nvidia官网](https://developer.nvidia.com/cuda-toolkit-archive)并选择对应`CUDA`版本

教程以`cuda 11.3.1`为例，按下图所示依次选择`Linux - x86_64 - Ubuntu - 1804 - runfile(local)`

{% asset_img cuda1.png %}

粘贴到服务器终端中执行

> 若下载速度慢，可以在自己电脑中下载后上传到机器中

{% asset_img cuda2.png %}

~~阅读完EULA后~~根据提示输入`accept`后回车

{% asset_img cuda3.png %}

根据提示把`Driver`去掉(上下键移动高亮到此处后按空格)后，移动到`Install`回车

{% asset_img cuda4.png %}

下一个提示也回车，之后耐心等待退出即可

{% asset_img cuda5.png %}

安装完成后会提示修改环境变量，需要添加以下两行到`~/.zshrc`末尾

```shell
export PATH=$PATH:{$PATH}
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:{$LD_LIBRARY_PATH}
```

> 推荐使用nano, `nano ~/.zshrc`，编辑后按`ctrl-x`，`y`，`回车`

{% asset_img cuda6.png %}

完成后可输入`nvcc -V`确认版本

{% asset_img cuda7.png %}

之后还需要在默认环境中卸载原来的PyTorch/Tensorflow并安装新的版本

{% asset_img cuda8.png %}

{% asset_img cuda9.png %} 

{% asset_img cuda10.png %} 
