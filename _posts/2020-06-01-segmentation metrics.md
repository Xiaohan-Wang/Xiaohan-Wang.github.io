---
layout:     post
title: 语义分割评价指标
subtitle:   
date:       2020-6-1
author:     Xiaohan
header-img: img/ice.jpg
catalog: true
tags:
    - Metrics
---

[//]: #(<img src="" width="100%" height="100%">)

#### 评价指标
Let $n_{ij}$ be the number of pixels of class $i$ predicted to belong to class $j$, where there are $n_{cl}$ different classes, and let $t_i=\sum_jn_{ij}$ be the total number of pixels of class $i$.

1. pixel accuracy: $\frac{\sum\limits_i n_{ii}}{\sum\limits_i t_{i}}$
2. mean pixel accuracy $\frac{1}{n_{cl}}\sum\limits_i \frac{n_{ii}}{ t_{i}}$
3. mean IoU: $\frac{1}{n_{cl}}\sum\limits_i \frac{n_{ii}}{t_i+\sum\limits_j n_{ji}-n_{ii}}$
4. frequency weighted IoU $\frac{1}{\sum\limits_k t_k}\sum\limits_i \frac{t_i n_{ii}}{t_i+\sum\limits_j n_{ji}-n_{ii}}$

#### Reference
1. Fully Convolutional Networks for Semantic Segmentation
