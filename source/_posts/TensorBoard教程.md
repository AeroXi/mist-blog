---
title: TensorBoard教程
date: 2020-07-27 12:23:00
tags:
---

[TensorBoard官方文档](https://github.com/tensorflow/tensorboard)

## 概述

TensorBoard是Tensorflow的可视化工具，它通过对Tensoflow程序运行过程中输出的日志文件进行可视化Tensorflow程序的运行状态。本文将介绍如何在服务器中启动TensorBoard，并从本地访问。

## 服务器端

首先从[**控制台**](https://mistgpu.com/user/)中**附加功能**一栏的**使用帮助**中获取服务器地址。

{% asset_img TB-1.png %}

在服务器信息一栏中可找到`主机名IP`和`开放端口`

{% asset_img TB-4.png %}

接下来进入到命令行中，输入`tensorboard --host 0.0.0.0 --port 开放端口 --logdir 日志文件目录`

例如这里开放端口是`30324`，则输入`tensorboard --host 0.0.0.0 --port 30324 --logdir /tmp`。

若有如下输出则表示成功启动：
{% asset_img TB-2.png %}

## 本地端

打开浏览器，在地址栏中输入```主机名:开放端口```，
如```gpu82.mistgpu.xyz:30324```。

成功访问：
{% asset_img TB-3.png %}