---
layout:     post
title: MobileNets
subtitle:  arXiv 2017 
date:       2020-5-15
author:     Xiaohan
header-img: img/ice.jpg
catalog: true
tags:
    - Baseline
---

[Paper link](https://arxiv.org/pdf/1704.04861.pdf)

[//]: #(<img src="" width="100%" height="100%">)

#### Take away message
1. MobileNets: light weight deep neural networks that use depth-wise separable convolutions
2. two simple global hyper-parameters that efficiently trade off between latency and accuracy

#### Model
##### Depth separable convolution
<img src="/img/15895586236484.jpg" width="50%" height="100%">
1. depthwise convolution: apply a single filter per each input channel
2. pointwise convolution: a simple 1×1 convolution to create a linear combination of the output of the depthwise layer

* MobileNets use both batchnorm and ReLU nonlinearities for both layers.
<img src="/img/15895586917635.jpg" width="50%" height="100%">
* computation cost
    * symbols
        * $D_F$: input feature size / output feature size
        * $D_K$: kernel size
        * $M$: input channels
        * $N$: outout channels
    * standard convolutions  
        <img src="/img/15895585271744.jpg" width="33%" height="100%">
    * depthwise separable convolutions  
        <img src="/img/15895588519425.jpg" width="50%" height="100%">
    * reduction in computation: MobileNet uses 3 × 3 depthwise separable convolutions, which uses between 8 to 9 times less computation than standard convolutions at only a small reduction in accuracy  
        <img src="/img/15895588852425.jpg" width="55%" height="100%">
        
##### Network structure
<img src="/img/15895692454944.jpg" width="55%" height="100%">
1. The first layer is a full convolution.
2. All layers are followed by a batchnorm and ReLU nonlinearity with the exception of the final fully connected layer which has no nonlinearity and feeds into a softmax layer for classification
3. Down sampling is handled with strided convolution in the depthwise convolutions as well as in the first layer.
4. A final average pooling reduces the spatial resolution to 1 before the fully connected layer.
5. Counting depthwise and pointwise convo- lutions as separate layers, MobileNet has 28 layers.

* MobileNets structure puts nearly all of the computation into dense 1×1 convolutions. This can be implemented with highly optimized general matrix multiply (GEMM) functions.

##### Tricks
1. contrary to training large models we use less regularization and data augmentation techniques because small models have less trouble with overfitting.
2. it was important to put very little or no weight decay (L2 regularization) on the depthwise filters since their are so few parameters in them.

#### Hyperparameter
##### Width Multiplier: Thinner Models
* The role of the width multiplier $\alpha$ is to thin a network uniformly at each layer (the number of input channels $M$ becomes $\alpha M$,  and the number of output channels $N$ becomes $\alpha N$) 
* The computational cost of a depthwise separable convolution with width multiplier $\alpha$:
    <img src="/img/15895698351332.jpg" width="50%" height="100%">
* $ \alpha \in (0, 1]$ with typical settings of 1, 0.75, 0.5 and 0.25.
* Width multiplier has the effect of reducing **computational cost** and **the number of parameters** quadratically by roughly $\alpha^2$.

##### Resolution Multiplier: Reduced Representation
* resolution multiplier $\rho$ is applied to the input image and the internal representation of every layer. In practice we implicitly set $\rho$ by setting the input resolution.
* the computational cost for the core layers with width multiplier $\alpha$ and resolution multiplier $\alpha$:
    <img src="/img/15895703362678.jpg" width="50%" height="100%">
* $\rho \in (0, 1]$, which is typically set implicitly so that the input resolution of the network is 224, 192, 160 or 128.
* Resolution multiplier has the effect of reducing **computational cost** by $\rho^2$.

#### Result
<img src="/img/15895706506529.jpg" width="60%" height="100%">


#### Further reference 
1. G. Hinton, O. Vinyals, and J. Dean. Distilling the knowledge in a neural network. arXiv preprint arXiv:1503.02531, 2015.