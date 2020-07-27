---
title: TensorBoard教程
date: 2020-07-27 12:23:00
tags:
---

# TensorBoard使用教程

## 概述

TensorBoard是Tensorflow的可视化工具，它通过对Tensoflow程序运行过程中输出的日志文件进行可视化Tensorflow程序的运行状态。本文将介绍如何在服务器中启动TensorBoard，并从本地访问。

## 服务器端

首先从[**控制台**](https://mistgpu.com/user/)中的ssh命令一栏中获取服务器地址，例如
`ssh mist@gpu112.mistgpu.xyz -p 10040`

其中地址为`gpu112.mistgpu.xyz`
{% asset_img TB-1.png %}
其次点击**附加功能-使用帮助**，获取开放端口。

接下来进入到命令行中，输入`tensorboard --logdir=日志文件目录 --host=0.0.0.0 --port=开放端口`

完整例子如下：`tensorboard --logdir=/tmp --host=0.0.0.0 --port=10044`

若有如下输出则表示成功启动：
{% asset_img TB-2.png %}

## 本地端

打开浏览器，在地址栏中输入```服务器地址:开放端口```，
如```gpu112.mistgpu.xyz:10044```。

成功访问：
{% asset_img TB-3.png %}