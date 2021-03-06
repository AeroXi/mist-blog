---
title: AI主播，在线解说：腾讯AI lab提出多模态语音合成模型DurIAN
date: 2020-02-10 19:45:55
tags:
---
## 论文笔记：腾讯AI lab多模态语音合成模型DurIAN
论文：[DurIAN: Duration Informed Attention Network For Multimodal Synthesis](https://arxiv.org/abs/1909.01700)，[演示地址](https://tencent-ailab.github.io/durian/)。

## 概述
DurIAN是腾讯AI lab于19年9月发布的一篇论文，主体思想和[FastSpeech](https://arxiv.org/abs/1905.09263)类似，都是抛弃attention结构，使用一个单独的模型来预测alignment，从而来避免合成中出现的跳词重复等问题，不同在于[FastSpeech](https://arxiv.org/abs/1905.09263)直接抛弃了autoregressive的结构，而DurIAN相当于一个去除Attention的Tacotron2/Tacotron，因为没有autoregressive，[FastSpeech](https://arxiv.org/abs/1905.09263)有了百倍的加速。除此以外，FastSpeech使用一个train好的[Transformer-TTS](https://arxiv.org/abs/1809.08895) model作为alignment信息的来源，而DurIAN使用Forced-alignment工具作为alignment信息的来源。DurIAN还利用语音+人脸特征点的数据集，让DurIAN在合成语音的同时预测对应的人脸特征点信息，从而实现AI虚拟人说话的效果；由于拥有不同情感标签的数据集，DurIAN进行了监督的情感学习，可以细粒度调整合成语音的情感，总而言之，[演示](https://tencent-ailab.github.io/durian/)的效果十分惊人。（paper中还提出了一种Multi-Band WaveRNN的结构，笔者对vocoder技术不是很熟悉，在这里就不做阐述了）

## 模型架构
模型整体结构如下图所示，去除Attention的方法大家可以参考[FastSpeech阅读笔记](https://zhuanlan.zhihu.com/p/67325775)和[Tacotron的paper](https://arxiv.org/abs/1703.10135)，本文主要说说paper中对中文的特殊处理办法和Style Code的部分。


{% asset_img model.PNG model %}

### 处理中文字符
为了可以让模型学到更多地韵律、停顿信息，DurIAN在text部分加入了特殊字符（之前看过别人做中文TTS，如果不手工在句子里面加间隔，合成出来的断句可能完全是不对的），一共加了四种不同的特殊字符，其中#S表示音位的间断，#1表示prosodic words的间断，#2表示prosodic phrase的间断，#3表示intonational phrase的间断，如下图。在encoder部分这些间断作为一个单独的vector，最后encoder output要去除表示这些间断的vector，因为Forced-alignment不会给这些vector做alignment，而在CBHG结构中已经考虑过上下文，这些间断的信息已经被包含在了其他vector中了，所以这里直接丢弃。


{% asset_img seq.PNG seq %}

### Style Code
paper中花了很大篇幅阐明了像VAE和GST这些unsupervised model中，对style信息进行提取所存在的问题，最大的问题就是**提取出来的style不具有实际意义**，很难被实际应用，所以paper中使用了supervised的方法，使用了包含多种情感标签的数据进行训练。在training的时候，每个情感标签进行one-hot编码乘以embedding，得到对应情感的embedding vector，在乘以一个learnable的Control Scale获得Style Code，Style Code在模型的两个部分进行concatenate，大家可以参考第一幅图。在inference阶段，可以调节one-hot编码，比如原本one-hot中表示开心是\[1, 0, 0, 0\]，而inference想要合成既有开心又有兴奋的语音，就可以改为\[0.5, 0, 0.5, 0\]，用这种方法，DurIAN可以对合成语音进行细粒度的情感控制。


{% asset_img style_code.PNG style %}

## 总结
这篇paper让我意识到“原来语音合成还可以这么玩”，合成的效果的确很惊艳，特别是配合AI虚拟人的时候。一句题外话，FastSpeech和DurIAN都借助了一个“teacher model”，可不可以做到直接训练呢？teacher model提供的alignment会对student model的performance有什么影响吗？
