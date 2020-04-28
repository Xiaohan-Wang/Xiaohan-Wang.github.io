---
layout: post
title: Fully Convolutional Networks for Semantic Segmentation
subtitle:   CVPR 2015
date:       2020-04-22
author:     Xiaohan
header-img: img/ice.jpg
catalog: true
tags:
    - Semantic Segmentation
---

[Paper link](https://arxiv.org/pdf/1411.4038.pdf) and [code (pytorch)](https://github.com/wkentaro/pytorch-fcn)

[//]: #(<img src="" width="100%" height="100%">)

#### Take away message
将分类网络中的全连接层变为对应的卷积层，从而得到全卷积网络。全卷积网络可用于实现如语义分割的稠密预测任务。添加skip-connecting结合deep, coarse, semantic information和shallow, fine, appearance information。

#### Model
1. 全连接层变为卷积层
<img src="/img/15876140745604.jpg" width="70%" height="70%">
    * view fully connected layers as convolutions with kernels that cover their entire input regions.
    * 优点：When receptive fields overlap significantly, both feedforward computation and back propagation are much more efficient when computed layer-by-layer over an entire image instead of independently patch-by-patch. （receptive field: locations in the image that locations in higher layers are path-connected to.）
    * 问题：由于subsampling, output的分辨率远低于input  
&nbsp;    

1. 转置卷积增大分辨率(what)+skip connection结合低层位置信息(where)
![-w870](/img/15876162869041.jpg)
    * 转置卷积能实现最好的上采样效果，通过learning可以实现非线性的上采样
    * 将upsampled结果 (deep, coarse, semantic information) 和skip connection结果 (shallow, fine, appearance information) 加起来，得到combine what and where的结果
    * Initialize the 2× upsampling to bilinear interpolation, but allow the parameters to be learned）。 但是，在FCN-8s后，继续融合低层信息取得的结果基本不变。因此，最后几层直接使用bilinear interpolation。

#### Result
##### 评价指标
Let $n_{ij}$ be the number of pixels of class $i$ predicted to belong to class $j$, where there are $n_{cl}$ different classes, and let $t_i=\sum_jn_{ij}$ be the total number of pixels of class $i$.
<img src="/img/15876175187934.jpg" width="40%" height="50%">
##### 结果
<img src="/img/15876184066437.jpg" width="50%" height="70%">

#### Tricks
1. 使用classification的网络参数作为预训练模型，在此基础上fine-tune网络以用于semantic segmentation任务。


