---
layout:     post
title: batch size与learning rate
subtitle: Accurate, Large Minibatch SGD:_Training ImageNet in 1 Hour
date:       2020-5-28
author:     Xiaohan
header-img: img/ice.jpg
catalog: true
tags:
    - Model Training
---

[Paper link](https://arxiv.org/pdf/1706.02677.pdf)

#### Take away message
1. 当满足一定条件下，batch_size增大k倍时，lr可以直接相应增大k倍
2. 训练初期不满足1)所需的条件，此时lr需要使用warm up
3. underlying loss function受batch size影响。为了不改变underlying loss function，在增大batch_size时，其实并不是改变per-worker sample size n，而是增大the number of workers k

#### Linear Scaling Rule
设有 k 个mini-batch $B_0, \cdots, B_{k-1}$: 
1. $lr=\eta$, 使用小batch_size $B_j$训练，共训 k 个iteration（$j=0, \cdots, k-1$）：  
    <img src="/img/15906983171534.jpg" width="40%" height="100%">
2. $lr = \hat{\eta}$, 使用大batch-size $\cup_j{B_j}$训一个iteration：
    <img src="/img/15906986727563.jpg" width="40%" height="100%">  

1和2对应不同的更新方式，因此不太可能有$\hat w_{t+1} = w_{t+k}$。但是，**如果我们假设$\nabla l(x,w_t) \approx \nabla l(x,w_{t+j})$ for $j < k$，那么在 $\hat \eta =k\eta$ 条件下能推出 $\hat w_{t+1} \approx  w_{t+k}$，即使用不同batch-size得到相似的更新结果**。

#### Warm up
在训练的开始阶段，模型权重迅速改变，不满足linear scaling rule中的条件。此时使用gradual warmup有助于解决训练中出现的问题。

#### Batch normalization
如果有BN层，那么每个sample的loss其实并不是独立的，而是与其所在的mini-batch有关（因为会根据每个mini-batch的mean/std做normalization）。由于不同的mini-batch size会导致不同的mean/variance statistics distribution，因此改变mini-batch size会改变underlying loss function。

为了不改变underlying loss function，根据上述分析，在增大mini-batch size时，我们其实不应该改变per-worker sample size n（batch statistics是在每个worker上单独计算的），而是应该增大the number of workers k。通常n=32在大部分数据集和网络上都表现良好。


