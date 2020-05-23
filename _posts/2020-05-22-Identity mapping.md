---
layout:     post
title: Identity mapping
subtitle:   ECCV 2016
date:       2020-5-22
author:     Xiaohan
header-img: img/ice.jpg
catalog: true
tags:
    - Baseline
---

[Paper link](https://arxiv.org/pdf/1603.05027.pdf)

[//]: #(<img src="" width="100%" height="100%">)

#### Take away message
The forward and backward signals can be directly propagated from one block to any other block, when using identity mappings as 1) the skip connections and 2) after-addition activation. This makes training easier and improves generalization.

#### Model
Residual unit:
<img src="/img/15902038485632.jpg" width="25%" height="100%">
* $x_l$ and $x_{l+1}$ are input and output of the $l$-th unit
* $F$ is a residual function
* $h(x_l) $ is an skip connection
* $f$ is an after-addition activation function.

**If (i) skip connection is identity mapping $h(x_l) = x_l$, and (ii) after-addition activation $f$ is an identity mapping, then we have
<img src="/img/15902041544783.jpg" width="30%" height="100%">
<img src="/img/15902041725422.jpg" width="50%" height="100%">
that is, the signal can be directly propagated from any unit to another, both forward and backward.**

##### Identity Skip Connections
<img src="/img/15902046739782.jpg" width="81%" height="100%">
<img src="/img/15902049097732.jpg" width="80%" height="100%">

As indicated by the grey arrows in Fig. 2, the shortcut connections are the most direct paths for the information to propagate. Multiplicative manipulations (scaling, gating, 1×1 convolutions, and dropout) on the shortcuts can hamper information propagation and lead to optimization problems.

##### Activation Functions
<img src="/img/15902048739817.jpg" width="80%" height="100%">
<img src="/img/15902048935542.jpg" width="80%" height="100%">
1. (a) original residual unit  
2. (b) BN after addition
    * the BN layer alters the signal that passes through the shortcut and impedes information propagation
3. (c) ReLU before addition
    * a non-negative output from the transform $F$, while intuitively a “residual” function should take values in $(-\infty, +\infty)$. As a result, the forward propagated signal is monotonically increasing, which may impact the representational ability.
4. pre-activation: develop an asymmetric form where an activation $f$ only affect the residual path but not the both paths in the next Residual Unit (i.e. move the activation module in a) and b) to the residual path, which become d) and e))
    * (d) This ReLU layer is not used in conjunction with a BN layer, and may not enjoy the benefits of BN.
    * (e)  result is good

Benefit of pre-activation  
1. Ease of optimization
    * the benefit of ease of optimization is more obvious in 1001-layer network than networks with fewer layers. 
2. Reducing overfitting
    * The pre-activation version reaches slightly higher training loss at convergence, but produces lower test error. This phenomenon is observed on ResNet-110, ResNet-110(1-layer), and ResNet-164 on both CIFAR-10 and 100.
    * In the original Residual Unit (Fig. 4(a)), although the BN normalizes the signal, this is soon added to the shortcut and thus the merged signal is not normalized. This unnormalized signal is then used as the input of the next weight layer. On the contrary, in the pre-activation version, the inputs to all weight layers have been normalized.
