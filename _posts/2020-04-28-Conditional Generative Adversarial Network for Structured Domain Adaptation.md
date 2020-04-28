---
layout:     post
title: Conditional Generative Adversarial Network for Structured Domain Adaptation
subtitle:   CVPR 2018
date:       2020-4-28
author:     Xiaohan
header-img: img/ice.jpg
catalog: true
tags:
    - Domain Adaptation
---

[Paper link](http://openaccess.thecvf.com/content_cvpr_2018/papers/Hong_Conditional_Generative_Adversarial_CVPR_2018_paper.pdf)

[//]: #(<img src="" width="100%" height="100%">)

#### Take away message
1. We shouldn't assume that the source and target domains share same intermediate feature space(s), i.e. using loss to obtain domain-invariant features.
2. Use a conditional generator to transform source feature maps into target-like, and trained on the target-like feature maps and original labels (和pixel level domain adaptation类似，但pixel level DA将source images转化为target-like，而本文将source features转化为target-like).
3. 文章中提到 without relying on the assumption that the source and target domains share a same prediction function in a domain-invariant feature space。 实际只完成了not in a domain-invariant feature space， 本质上还是same prediction function (source和target domain的encoder和decoder都相同)

#### Model
![-w913](/img/15881099962969.jpg)
1. a conditional generator to generate residual features, to transform features of synthetic images to real-image like features.
    * a noise map $z$ is addd for randomness to create an unlimited number of training samples.
    * expect that $x_f$ preserves the semantic of the source feature map $x_s$, meanwhile appears as if it were extracted from a target domain image, i.e., a real image. 
2. a discriminator to distinguish adapted source features and real target features.
3. task-specific loss (decoder part)
    * train T with both adapted and non-adapted source feature maps (Training T solely on adapted feature maps leads to similar performance, but requires many runs with different initializations and learning rates due to the instability of the GAN).
4. overall minimax objective:  
<img src="/img/15881108285954.jpg" width="50%" height="100%">

#### Result
1. overall performance: 涨幅非常大  
![-w905](/img/15881108796823.jpg)

1. amount of synthetic data
 <img src="/img/15881109617007.jpg" width="50%" height="100%">

1. Ablation Studies
    * The effectiveness of conditional generator  
    <img src="/img/15881110275006.jpg" width="50%" height="100%">

    * Different lower layers for learning generator
    <img src="/img/15881111038400.jpg" width="60%" height="100%">
    * On the number of residual blocks （上图）
    * How much does the noise channel contribute?
    <img src="/img/15881111498987.jpg" width="50%" height="100%">


