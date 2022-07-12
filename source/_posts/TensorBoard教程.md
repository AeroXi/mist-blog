---
title: TensorBoard教程
date: 2020-07-27 12:23:00
tags:
---

[TensorBoard官方文档](https://github.com/tensorflow/tensorboard)

# 服务器端

在控制台的**附加功能**中点击使用帮助，复制`IP`及`开放端口`。

{% asset_img help.png %}

{% asset_img tb1.png %}

接下来进入到服务器命令行中，输入
```text
tensorboard --host 0.0.0.0 --port {开放端口} --logdir {日志文件目录}
```

本例的开放端口是`12605`，日志文件在`log/fit/`下，
则输入 `tensorboard --host 0.0.0.0 --port 30324 --logdir log/fit`

若有如下输出则表示成功启动：

{% asset_img tb2.png %}

# 本地端

打开本地浏览器，在地址栏中输入
```text
主机名:开放端口
```

如本例输入 `gpu294.mistgpu.com:12605`

成功访问：
{% asset_img tb3.png %}

# 日志文件目录

Tensorboard日志文件一般在代码中有设置，如果不确定的话可以找哪些文件夹下有`events.out.tfevents`文件

{% asset_img tb4.png %}
