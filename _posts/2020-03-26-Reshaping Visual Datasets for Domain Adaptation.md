---
layout:     post
title: Reshaping Visual Datasets for Domain Adaptation
subtitle:   NIPS 2013
date:       2020-3-26
author:     Xiaohan
header-img: img/ice.jpg
catalog: true
tags:
    - Domain Adaptation
---

[Paper link](http://papers.nips.cc/paper/5210-reshaping-visual-datasets-for-domain-adaptation.pdf)

[//]: #(<img src="/img/15852773040000.jpg" width="100%" height="100%">)

<img src="/img/15852773040000.jpg" width="100%" height="100%">
#### Take away message
图像的domain由多种因素交织影响决定，比如说pose、illumination、camera resolution、background等等。因此图像往往不是按照“clearly identifiable domain”收集的，也就是说，一个数据集可以包含多个不同的domain。发现这些source和target dataset中的latent domain有助于进行domain adaptation.

#### Model
> Note that the total domain distinctiveness TDD(K) increases as K increases — presumably, in the extreme case, each domain has only a few instances and their distributions would be maximally different from each other. However, such tiny domains would offer insufficient data to separate the categories of interest reliably.

1. maximum distinctiveness: 希望不同domain之间的差异尽量大 (domain划分尽量细)  

    采用non-parameter方式:  
    * the empirical distribution of each domain:
    <img src="/img/15852779640661.jpg" width="100%" height="100%">
    * the difference between the means of two empirical distributions
    ![-w837](/img/15852781025087.jpg)
    * maximize the total domain distinctiveness
    <img src="/img/15852781836513.jpg" width="30%" height="30%">

1. maximum learnability: 每个domain包含足够数量的instances用于学习 (domain划分不能过细)

    从K=2开始遍历寻找最好的K
    * 对K个domain分别构建classfier，并计算cross-validation accuracy，并求weighted average
    ![-w699](/img/15852795347553.jpg)

    * 选择具有最高的cross-validation accuracy的K

#### Result
domain adaptaion的几种方式
1. 合并全部source domain
2. emsemble各个source domain的classfier的结果
3. 选择和target domain最接近的一个source domain
4. reshape target domain conditioning on the identified domains from the training datasets — the goal is to discover latent domains in the test datasets that match the domains in the training datasets as much as possible.
![-w752](/img/15852803974334.jpg)

    <img src="/img/15852803845757.jpg" width="93%" height="93%">


#### Further reference
1. J. Hoffman, B. Kulis, T. Darrell, and K. Saenko. Discovering latent domains for multisource domain adaptation. In ECCV. 2012. (aim at discovering the latent domains from datasets, by modeling the data with a hierarchical distribution consisting of Gaussian mixtures)


