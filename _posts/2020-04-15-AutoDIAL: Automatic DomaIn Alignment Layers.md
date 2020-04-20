---
layout: post
title: AutoDIAL:Automatic DomaIn Alignment Layers
subtitle:   ICCV 2017
date: 2020-04-15
author: Xiaohan
header-img: img/ice.jpg
catalog: true
tags:
    - Domain Adaptation
---

[Paper link](https://arxiv.org/pdf/1704.08082.pdf) and [code](https://github.com/ducksoup/autodial)

[//]: #(<img src="" width="100%" height="100%">)

#### Take away message
1. limitation of AdaBN: the target samples have no influence on the network parameters, as they are not observed during training.
2. 对训练过程描述的很详细，可以参考

#### Model
![-w821](/img/15873547625687.jpg)

<img src="/img/15873551722703.jpg" width="25%" height="100%"><img src="/img/15873552325041.jpg" width="25%" height="100%"><img src="/img/15873552520236.jpg" width="50%" height="100%">  
其中， $\alpha$ 在[0.5, 1]中：1对应AdaBN (full degree of DA)；0.5对应没有DA，因为此时$q_\alpha^{st}$和$q_\alpha^{ts}$相同，即source和target domain会做相同的transformation。通过让网络自己学习参数$\alpha$，实现了automatically learn the degree of alignment that should be pursued at different levels of the network.

#### Tricks
Bayes based training process:  
1. objective:  
<img src="/img/15873556873967.jpg" width="45%" height="100%"><img src="/img/15873557363954.jpg" width="30%" height="100%">  
1. sampling distribution  
<img src="/img/15873558553822.jpg" width="35%" height="100%">  
1. prior
<img src="/img/15873559027282.jpg" width="45%" height="100%">  
<img src="/img/15873559171140.jpg" width="45%" height="100%">  

4. 转化为training objective：
<img src="/img/15873559673684.jpg" width="45%" height="100%">    
source domain用standard cross entropy loss， target domain用entropy minimization.


#### Result
1. $\alpha$ 大部分接近1.  
![-w907](/img/15873565357251.jpg)  

others:
1. the entropy regularization term is especially beneficial when source and target data representations are aligned. (?)
2. lower layers in a network are subject to domain shift even more than the very last layers.

#### Reflection
1. 同时结合了AdaBN和entropy minimization， 不确定结果的提高是否来源于提出的DA layer.




