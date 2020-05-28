---
layout:     post
title: Learning rate scheduler
subtitle:   
date:       2020-5-28
author:     Xiaohan
header-img: img/ice.jpg
catalog: true
tags:
    - Model Training
---

[//]: #(<img src="" width="100%" height="100%">)

#### Warm up
1. 减缓模型在训练初期过拟合mini-batch    
    个人猜测：
    * 在第一轮训练的时候（尤其是训练刚开始），模型只见过部分数据，此时梯度大概率是偏离相对全局真正较优的方向的（此时很大概率是过拟合当前小部分数据的方向），因此需要使用较小的学习率，以免对当前小部分数据过拟合，对后面训练造成影响（影响有两种可能：1）需要后面多轮训练来修正之间的偏差；2）偏差太大，后面多轮训练也没用，最后accuracy下降）。
    * 当训练了一段时间（比如两轮、三轮）后，模型见过了全部数据，此时梯度基本符合相对全局真正较优的方向，所以可以适当调大学习率。
2. 有助于保持模型深层的稳定性

#### Learning rate decay
学习率衰减的基本思想是学习率随着训练的进行逐渐衰减，即在开始的时候使用较大的学习率，加快靠近最小值的速度，在后来些时候用较小的学习率，提高稳定性，避免因学习率太大跳过最小值，保证能够收敛到最小值。

1. step(固定步长衰减): 每隔step_size个epoch后，lr衰减为原来的gamma倍

    <img src="/img/15906775729941.jpg" width="50%" height="100%">


    
1. multistep(多步长衰减): 动态步长控制，lr衰减为原来的gamma倍
     
     <img src="/img/15906776874073.jpg" width="50%" height="100%">

     
1. poly(多项式衰减): $lr = \text{base_lr} * (1 - \frac{T_{cur}}{T_{max}}) ^ {power} $
    * 学习率曲线的形状主要由参数 power 的值来控制。当 power = 1 的时候，学习率曲线为一条直线。当 power < 1 的时候，下降速率由慢到快。当 power > 1 的时候，下降速率由快到慢。
    <img src="/img/15906784236558.jpg" width="50%" height="100%">
    

1. cosine(余弦衰减): $lr = \frac{1}{2}*\text{base_lr} * \left(1+ \cos\left(\frac{T_{cur}}{T_{max}}\pi\right)\right)$
    * 余弦值首先缓慢下降，然后加速下降，之后再次缓慢下降。
    
    <img src="/img/15906782692333.jpg" width="50%" height="100%">
   
    
#### 参考资料
1. https://www.zhihu.com/question/338066667
2. https://lumingdong.cn/setting-strategy-of-gradient-descent-learning-rate.html
3. https://zhuanlan.zhihu.com/p/39565465


