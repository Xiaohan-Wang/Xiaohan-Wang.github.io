---
layout:     post
title: Maximum Classifier Discrepancy for Unsupervised Domain Adaptation
subtitle:   CVPR 2018 oral
date:       2020-4-10
author:     Xiaohan
header-img: img/ice.jpg
catalog: true
tags:
    - Domain Adaptation
---

[Paper link](https://arxiv.org/pdf/1712.02560.pdf) and [code](https://github.com/mil-tokyo/MCD_DA)

[//]: #(<img src="" width="100%" height="100%">)

#### Take away message
1. if only consider distribution matching (based on statistics), a trained generator can generate ambiguous features near class boundaries (在class boundary附近，由于缺少训练数据，相当于随机分类)
<img src="/img/15873584186697.jpg" width="80%" height="80%">

For better distribution alignment:
1. maximize the discrepancy between two classifiers’ outputs to detect target samples that are far from the support of the source.
2. A feature generator learns to generate target features near the support to minimize the discrepancy, in order to avoid generating target features near class boundaries.

#### Model
![-w775](/img/15873586517441.jpg)

##### discrepancy loss
use the absolute values of the difference between the two classifiers’ probabilistic outputs as discrepancy loss.
<img src="/img/15873624804347.jpg" width="30%" height="100%">

##### Training step
1. task-specific loss  
train both classifiers and generator to
classify the source samples correctly. In order to make classifiers and generator obtain task-specific discriminative features, this step is crucial.  
<img src="/img/15873636378997.jpg" width="25%" height="100%">
<img src="/img/15873636851548.jpg" width="55%" height="100%">

1. train classifier  
A classification loss on the source samples is added here. Without this loss, the authors experimentally found that our algorithm’s performance drops significantly.
<img src="/img/15873638777096.jpg" width="50%" height="100%">  

1. train generator
<img src="/img/15873639472583.jpg" width="15%" height="100%">

#### Reflection
1. distribution alignment也可以用adversarial learning来实现。adversarial learning自由度更大，相比于传统的基于参数的hand-crafted transformation， 也许更能实现理想的distribution alignment.



