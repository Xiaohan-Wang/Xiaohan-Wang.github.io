---
layout:     post
title: RefineNet:_Multi-Path Refinement Networks for High-Resolution Semantic Segmentation
subtitle:   CVPR 2017
date:       2020-5-9
author:     Xiaohan
header-img: img/ice.jpg
catalog: true
tags:
    - Semantic Segmentation
---

[Paper link](https://arxiv.org/pdf/1611.06612.pdf)

[//]: #(<img src="" width="100%" height="100%">)

#### Take away message
1. 设计RefineNet，结合高层语义信息和低层细节信息，得到高分辨率的分割图
2. RefineNet中大量使用了ResNet中Identity mapping (both short range and long range) 的思想，保证了有效的端到端训练

#### Introduction
网络中pooling操作会降低分割图的分辨率，目前有三种解决方式：
1. learn deconvolutional filters as an up-sampling operation: The deconvolution operations are not able to recover the low-level visual features which are lost after the downsampling operation in the convolution forward stage.
2. Deeplab系列中的atrous convolution: __a significant cost in memory, because unlike the image subsampling methods, one must retain very large numbers of feature maps at higher resolution.__ In practice, therefore, dilation convolution methods usually have a resolution prediction of no more than 1/8 size of the original rather than 1/4, when using a deep network.
3. exploits features from intermediate layers for generating high-resolution prediction (本文基于的方法)

#### Model
<img src="/img/15890589297975.jpg" width="70%" height="100%">
<img src="/img/15890589494152.jpg" width="100%" height="100%">

#### Result
<img src="/img/15890590750133.jpg" width="50%" height="100%">    

<img src="/img/15890590946983.jpg" width="50%" height="100%">    

<img src="/img/15890591146152.jpg" width="100%" height="100%">

#### Reflection
感觉整个网络设计并没有太新颖的模块或思路，但可能是通过大量的identity mapping达成了有效的端对端训练，最后得到了非常棒的结果。如果是的话，说明设计网络时，网络各个模块能否得到充分的训练非常重要。