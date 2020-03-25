---
layout:     post
title: Domain Adaptation for Semantic Segmentation with Maximum Squares Loss
subtitle:   ICCV 2019 
date:       2020-3-24
author:     Xiaohan
header-img: img/ice.jpg
catalog: true
tags:
    - Domain Adaptation
---

[Paper link](http://openaccess.thecvf.com/content_ICCV_2019/papers/Chen_Domain_Adaptation_for_Semantic_Segmentation_With_Maximum_Squares_Loss_ICCV_2019_paper.pdf) and [code](https://github.com/ZJULearning/MaxSquareLoss)

[//]: #(<img src="/img/15850315456104.jpg" width="40%" height="40%">)

#### Take away message
Probability imbalance problem -> maximum square loss

#### Probability imbalance problem
<img src="/img/15851597726007.jpg" width="70%" height="70%" >
Note that uncertain area has prediction probability around 0.5, while prediction probability around 1 corresponds to areas with good accuracy.

Shannon entropy:
<img style="text-align: center" src="/img/15851603980105.jpg" width="50%" height="50%" >
Maximum squares loss:
<img style="text-align: center" src="/img/15851604671115.jpg" width="45%" height="45%" >

Classes with high accuracy always have higher prediction probabilities. If Shannon entropy is deployed, as shown in the above figure, the simple class will produce a much larger gradient on each pixel than the difficult class, causing each gradient descent step is basically computed from those simple classes, and difficult classes is still not trained sufficiently. By using MSL, areas with higher confidence still have larger gradients, but their dominant effects have been reduced, allowing other difficult classes to obtain training gradients.

#### Class imbalance problem
Classes with higher accuracy always have more pixels on the label map, which leads to an imbalance in quantity.

regular method: introduce weighting factor αc, which is usually set as the inverse class frequency.

paper: Image-wise Class-balanced Weighting Factor

#### Tricks
1. fix class imbalance 
    * regular way: introduce weighting factor αc, which is usually set as the inverse class frequency.
    * image-wise weighting ratio (this paper)
2. multi-level self-produced guidance


