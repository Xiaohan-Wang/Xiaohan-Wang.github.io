---
layout:     post
title:      Domain Adaptation Concept Summary
subtitle:   
date:       2020-03-14
author:     Xiaohan
header-img: img/ice.jpg
catalog: true
tags:
    - Domain Adaptation
    - Concept
---

### Transfer learning
#### domain and task
1. domain = feature space + marginal distribution
2. task = label space + conditional distribution (predictive function)

#### transfer learning定义
![-w914](/img/15842471547628.jpg)
1. 正常的machine learning: 只有一个domain，通过自己的X、Y学习predictive function
2. transfer learning：利用source的知识提高target的predictive function的表现
    * source和target是不同的
        * feature space不同 
        * marginal distribution不同
        * label space不同    
        * conditional distribution不同  （？？）
3. _domain adaptation_: transfer learning的子类，source和target只有marginal distribution不同，其余三点都相同

#### Domain adaptation
![](/img/15850826248103.jpg)
from https://en.wikipedia.org/wiki/Domain_adaptation

