---
layout:     post
title: Distilling the Knowledge in a Neural Network
subtitle:   NIPS 2014 workshop
date:       2000-1-1
author:     Xiaohan
header-img: img/ice.jpg
catalog: true
tags:
    - Knowledge Distillation
---

[Paper link](https://arxiv.org/pdf/1503.02531.pdf) 

[//]: #(<img src="" width="100%" height="100%">)



#### Take away message
1. transfer the knowledge from the cumbersome model (used in training stage) to a small model (suitable for deployment)
2. **"knowledge": a learned mapping from input vectors to output vectors** 
    * use the class probabilities produced by the cumbersome model as “soft targets” for training the small model.
3. **small probabilities in the soft targets define a rich similarity structure over the data, but it has very little influence on the cross-entropy cost function during the transfer stage because the probabilities are so close to zero**.
    * use “distillation” to raise the temperature of the final softmax until the cumbersome model produces a suitably soft set of targets.
4. adding a small term to the objective function that encourages the small model to **predict the true targets as well as matching the soft targets provided by the cumbersome model** works pretty well.

#### Model
##### 整体思路：
* 想要transfer的knowledge是从input到output的映射。也就是说，对于相同的input，希望cumbersome model和small model能生成相同的output (soft label)
* 用cumbersome model和small model产生的soft label做cross entropy loss
    * 问题：除了hard target对应的概率，其它负标签的概率其实也提供了大量的信息。比如说一张2的图片，对应3的soft label是1e-6，而7的soft label是1e-9，说明这张图片除2之外，更像3而不像7。但是，如果使用传统的softmax层 (T=1)，我们很难有效利用这些信息，因为这些负标签的soft label太小了，基本不能影响cross entropy loss的结果
    * 为了能利用负标签对应概率所提供的信息，使用distillation，通过增大T来产生softer probability distribution，此时正负标签对应的soft label差距将被缩小，因此负标签的soft label也能影响最终的cross entropy loss

##### 知识蒸馏
* 带温度T的softmax表达式：

    $$q_{i}=\frac{\exp \left(z_{i}/T\right)}{\sum_{j} \exp \left(z_{j}/T \right)}$$
    
* 温度T的影响  
    <img src="/img/15928689216135.jpg" width="70%" height="100%">  
    * 原始的softmax函数是 $T=1$ 时的特例
    * 温度越高，softmax后各个值z的分布就越平均，原本较小的soft label此时相对增大，对最终cross entropy loss的影响增大，也就提高了对这些原本soft label较小的负标签的关注程度
* 如何选择温度T
    * 不是所有的负标签对应的soft label都是有效的：这些soft label本身是由Teacher-Net (cumbersome model) 训练得到的，因此结果一定存在noise，而且soft label越小，noise的影响越大
    * 温度T决定了对负标签的关注程度
        * 从有部分信息量的负标签中学习 --> 温度要高一些
        * 防止受负标签中噪声的影响 -->温度要低一些

##### 知识蒸馏方法
<img src="/img/15928705010652.jpg" width="70%" height="100%">  
1. 训练Teacher model
2. 对Teacher model蒸馏，得到student distilled model
    * soft prediction loss：Teacher model和 Student model在相同温度T下产生的soft label的cross entropy loss
    * hard prediction loss：Student model在T=1时和groundtruth的cross entropy loss

#### Note
1. the magnitudes of the gradients produced by the soft targets scale as $\frac{1}{T^2}$, so it is important to multiply them by $T^2$ when using both hard and soft targets
2. matching logits is a special case of distillation

#### 参考资料
1. [知识蒸馏](https://zhuanlan.zhihu.com/p/102038521)
2. [交叉熵与KL散度](https://zhuanlan.zhihu.com/p/61944055)