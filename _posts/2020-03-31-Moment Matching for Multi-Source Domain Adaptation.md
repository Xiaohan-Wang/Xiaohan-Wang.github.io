---
layout:     post
title: Moment Matching for Multi-Source Domain Adaptation
subtitle: ICCV 2019  
date:       2020-3-31
author:     Xiaohan
header-img: img/ice.jpg
catalog: true
tags:
    -  Domain Adaptation
---

[Paper link](http://openaccess.thecvf.com/content_ICCV_2019/papers/Peng_Moment_Matching_for_Multi-Source_Domain_Adaptation_ICCV_2019_paper.pdf) and [code](http://ai.bu.edu/M3SDA/)

[//]: #(<img src="" width="100%" height="100%">)

#### Take away message
1. the upper bound on the target error of the learned hypothesis depends on the pairwise moment divergence $d_{CM^k}(D_S, D_T)$ between the target domain and each source domain. (This provides a direct motivation for moment matching approaches)
2. The last term target error is lower bounded by the pairwise divergences between source domains (implies we might also need to minimize divergence between source domains)
3. DomainNet: multi-souce domain adaptation dataset

#### Model
![-w909](/img/15857182767863.jpg)

1. moment distance based loss:  
<img src="/img/15857184320957.jpg" width="60%" height="100%">
1. overall training objective:  
<img src="/img/15857185193833.jpg" width="50%" height="100%">
1. In order to align $p(y;x)$ and $p(x)$ at the same time, they follow the training paradigm proposed in [1]. They leverage two classifiers per domain to form N pairs of classifiers $C′ = {(C1, C1′), (C2, C2′), ..., (CN, CN ′)}$. The training procedure includes three steps. 
    1. train $G$ and $C′$ to classify the multi-source samples correctly based on the overall training objective.
    2. train the classifier pairs for a fixed $G$. The goal is to make the discrepancy of each pair of classifiers as large as possible on the target domain. 
    3. fix $C′$ and train $G$ to minimize the discrepancy of each classifier pair on the target domain.
    
#### Result
![-w781](/img/15857191596055.jpg)

![-w851](/img/15857190392968.jpg)个人感觉主要是$M^3SDA-\beta$中的training paradigm在发挥作用。

#### Further reference 
1. Kuniaki Saito, Kohei Watanabe, Yoshitaka Ushiku, and Tat- suya Harada. Maximum classifier discrepancy for unsuper- vised domain adaptation. In The IEEE Conference on Com- puter Vision and Pattern Recognition (CVPR), June 2018.
2. Chun-Liang Li, Wei-Cheng Chang, Yu Cheng, Yiming Yang, and Barnab´as P´oczos. Mmd gan: Towards deeper understanding of moment matching network. In Advances in Neural Information Processing Systems, pages 2203–2213, 2017.
3. Yujia Li, Kevin Swersky, and Rich Zemel. Generative mo- ment matching networks. In International Conference on Machine Learning, pages 1718–1727, 2015.
4. Youssef Mroueh, Tom Sercu, and Vaibhava Goel. McGan: Mean and covariance feature matching GAN. In Doina Pre- cup and Yee Whye Teh, editors, Proceedings ofthe 34th In- ternational Conference on Machine Learning, volume 70 of Proceedings of Machine Learning Research, pages 2527– 2535, International Convention Centre, Sydney, Australia, 06–11 Aug 2017. PMLR.

2，3，4是Gan based moment matching 

