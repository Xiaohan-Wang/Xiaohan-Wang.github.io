---
layout:     post
title:      Unsupervised Domain Adaptation using Feature-Whitening and Consensus Loss
subtitle:   CVPR 2019
date:       2020-03-14
author:     Xiaohan
header-img: img/ice.jpg
catalog: true
tags:
    - Domain Adaptation
---

[paper](https://arxiv.org/pdf/1903.03215.pdf) and [code](https://github.com/roysubhankar/dwt-domain-adaptation)
### Take Away Message
1. Domain alignment layers which implement feature whitening for the purpose of matching source and target feature distributions and increases the smoothness of the loss landscape.
2. Min-Entropy Consensus loss regularizes training while avoiding the adoption of many user-defined hyper-parameters

### Model
![-w752](/img/15843077382687.jpg)


DA的四种方法：
1. Correlation Alignment paradigm
2. domain-specific alignment layers
3. entropy minimization distribution
4. consistency-enforcing paradigm  

由 12 -> DWTL layer  
由 34 -> MEC loss

source: cross-entropy loss
![-w200](/img/15843177084504.jpg)
target: MEC loss
![-w300](/img/15843177196984.jpg)
final loss:
![-w300](/img/15843177315198.jpg)
1. 要求在source上表现好
2. 要求在target上对perturbation具有robustness，同时对结果high confidence

### Result 
1. digit classification
2. object recognition

### Potential Improvement
1. try full "coloring"
2. MEC loss中pseudo label的选择方式？