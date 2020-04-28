---
layout:     post
title: SegNet:_A Deep Convolutional Encoder-Decoder Architecture for Image Segmentation
subtitle: TPAMI 2017 (Arxiv 2015)
date:       2020-4-27
author:     Xiaohan
header-img: img/ice.jpg
catalog: true
tags:
    - Semantic Segmentation
---

[Paper link](https://arxiv.org/pdf/1511.00561.pdf)

[//]: #(<img src="" width="100%" height="100%">)

#### Take away message
1. In practice, we have to consider the cost of memory and computational time. 
2. Most recent deep architectures for segmentation have identical encoder networks, i.e VGG16, but differ in the form of the decoder network, training and inference.

#### Model
![-w901](/img/15880309668474.jpg)


Encoder:   
1. The encoder network consists of 13 convolutional layers which correspond to the first 13 convolutional layers in the VGG16 network. 
2. Initialize the training process from weights trained for classification on large datasets.
3. Benifit: Removing the fully connected layers of VGG16 makes the SegNet encoder network significantly smaller [reduces the number of parameters in the SegNet encoder network significantly (from 134M to 14.7M)] and easier to train.

Decoder:
<img src="/img/15880312579950.jpg" width="60%" height="100%">
1. The appropriate decoder in the decoder network upsamples its input feature map(s) using the memorized max-pooling indices from the corresponding encoder feature map(s). This step produces sparse feature map(s).
2. These feature maps are then convolved with a trainable decoder filter bank to produce dense feature maps.
3. Except for the last decoder (which corresponds to the first encoder), the other decoders in the network produce feature maps with the same number of size and channels as their encoder inputs.

#### Tricks
class balancing



