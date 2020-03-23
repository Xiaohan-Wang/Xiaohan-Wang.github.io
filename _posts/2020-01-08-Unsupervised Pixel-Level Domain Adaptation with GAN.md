---
layout:     post
title:      Unsupervised Pixel-Level Domain Adaptation with Generative Adversarial Networks
subtitle:   CVPR 2017
date:       2020-01-08
author:     Xiaohan
header-img: img/ice.jpg
catalog: true
tags:
    - Domain Adaptation
---
### Idea
* 适用于domain间存在low-level difference的domain adaptation
* 不需要domain间的corresponding pairs

### Model
![-w857](/img/15785106924617.jpg)
![-w50](/img/15785107411179.jpg){:height="100px" width="400px"}

主要由discriminator(D)来学习，classifier(T: task)和content-similarity loss主要用来 stabalize GAN的训练
* context-similarity loss: PMSE (pairwise mean squared error)
> This loss allows the model to learn to reproduce the overall shape of the objects being modeled without wasting modeling power on the absolute color or intensity of the inputs, while allowing our adversarial training to change the object in a consistent way.

### Reflection
1. T的参与感觉让domain adaptation变成了迎合任务的domain adaptation, 而不是单纯的pixel-level domain adaptation. (也有优势，在对应任务上应该有更好的表现)