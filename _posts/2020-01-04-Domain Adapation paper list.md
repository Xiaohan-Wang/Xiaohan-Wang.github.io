---
layout:     post
title:      Domain Adaptation Paper List
subtitle:   持续更新中
date:       2020-01-04
author:     Xiaohan
header-img: img/post-bg-2015.jpg
catalog: true
tags:
    - Domain Adaptation
    - Paper List
---
### Dataset
1. [Unbiased look at dataset bias](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=5995347) (CVPR 2011) [*link*](https://xiaohan-wang.github.io/2020/01/05/Unbiased-Look-at-Dataset-Bias/)

### DA Approaches
![-w870](/img/15842344918937.jpg)

#### images mapping
1. [Pixel-Level Domain Transfer](https://arxiv.org/pdf/1603.07442.pdf) (ECCV 2016) [*link*](https://xiaohan-wang.github.io/2020/01/07/Pixel-Level-Domain-Transfer/)
    * need corresponding pairs between two domains (essentially supervised)
    * 但认为MSE never allow a small geometric miss-alignment，因此使用discriminator来利用supervised information
    * 未提及gt的变化

2. [Unsupervised Pixel–Level Domain Adaptation
with Generative Adversarial Networks](https://arxiv.org/pdf/1612.05424.pdf) (CVPR 2017) [*link*](https://xiaohan-wang.github.io/2020/01/08/Unsupervised-Pixel-Level-Domain-Adaptation-with-GAN/)
 * assume that the difference between the domains are primarily low-level (due to noise, resolution, illumination, color) rather than high-level (types of objects, geometric variations, etc)
 * 未提及gt的变化

1. [Learning from Simulated and Unsupervised Images through Adversarial Training](https://arxiv.org/pdf/1612.07828.pdf) （CVPR 2017）
    * gt不变
 
#### domain specific network

#### domain-invariant representation
1. [Deep Domain Confusion: Maximizing for Domain Invariance](https://arxiv.org/pdf/1412.3474.pdf) (arXiv 2014)  
    * classification loss + MMD loss
2. [Deep CORAL: Correlation Alignment for Deep Domain Adaptation](https://arxiv.org/pdf/1607.01719.pdf)（Computer Vision – ECCV 2016 Workshops） 
    * classification loss + coral loss  
    * minimize the difference in second-order statistics between the source and target feature activations (CORAL loss)
