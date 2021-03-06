---
layout:     post
title:  EM algorithm, K-means, and GMM
subtitle: 
date:       2020-6-9
author:     Xiaohan
header-img: img/ice.jpg
catalog: true
tags:
    - Clustering
---

#### EM algorithm
* EM算法是期望最大化(Expectation Maximization)算法的简称
* 用于**含有隐变量(hidden variable)**的情况下，模型参数的最大似然估计
* EM算法是一种迭代算法，每次迭代由两步组成：
    * E步：根据模型参数的假设值，给出隐变量的期望估计，应用于缺失值
    * M步：根据隐变量的估计值，给出当前的参数的极大似然估计

#### K-means
1. 先随机选定k个点作为质心 $\mu_1, \mu_2, \cdots, \mu_𝑘$
2. E step: 固定$\mu_k$，将样本划分到距离最近的$\mu_k$所属的簇中  

    $$r_{nk} = \left. \begin{cases} 1 \,\, & \text{if} \;\;\;k = \mathop{argmin}_j ||\mathbf{x}_n - \boldsymbol{\mu}_j||^2 \\
0 \,\, & \text{otherwise} \end{cases} \right.$$

1. M step: 对于每一个数据簇，重新计算其中心，目标是最小化簇中每个样本与中心的距离，可表示为 

    $$J = \sum\limits_{n=1}^N r_{nk} ||\mathbf{x}_n - \boldsymbol{\mu}_k||^2.$$
    
    为求得最小化 $J$ 的 $\mu_k$，可通过 
    
    $$\frac{\partial J}{\partial\mathbf{\mu}_k}=2\sum\limits_{n=1}^N r_{nk}(\boldsymbol{x}_n - \boldsymbol{\mu}_k) = 0,$$
    
    求得
    
    $$\boldsymbol{\mu}_k = \frac{\sum_nr_{nk} \mathbf{x}_n}{\sum_n r_{nk}},$$
    
    即簇中每个样本的均值向量。
1. 重复计算 E-step 和 M-step 直至收敛


#### Gaussian Mixture Model (GMM)
* 混合模型 (mixture model)：是一个可以用来表示在总体分布中含有 K 个子分布的概率模型。换句话说，总体的概率分布，是一个由 K 个子分布组成的混合分布。
    * 混合模型不要求观测数据提供其属于哪个子分布 => hiddle varibale
    * **对于混合模型来说，每个子分布天然地构成了各自的一类**
* 高斯混合模型：由 K 个单高斯模型组合而成的模型。一般来说，一个混合模型可以使用任何概率分布，这里使用高斯混合模型是因为高斯分布具备很好的数学性质以及良好的计算性能。
    * 高斯混合模型的概率分布为：

        $$P(x|\theta) = \sum_{k=1}^{K}{\alpha_{k}\phi(x|\theta_{k})}$$
    * 对于这个模型而言，参数 $\theta = (\tilde{\mu_{k}}, \tilde{\sigma_{k}}, \tilde{\alpha_{k}})$ ，也就是每个子模型的期望、方差（或协方差）、在混合模型中发生的概率
    * 如果通过使用足够多的高斯分布，并且调节它们的均值和方差以及线性组合的系数，那么几乎所有的连续概率密度都能够以任意的精度近似。

    
1. 随机初始化模型参数（各个高斯分布的均值、方差、发生概率）
2. E step: 依据当前参数，计算每个数据 $j$ 来自子模型 $k$ 的可能性

    $$\gamma_{jk} = \frac{\alpha_{k}\phi(x_{j}|\theta_{k})}{\sum_{k=1}^{K}{\alpha_{k}\phi(x_{j}|\theta_{k})}}, j = 1,2,...,N; k = 1,2,...,K$$

1. M step: 计算新的模型参数

    $$\mu_{k} = \frac{\sum_{j=1}^{N}{(\gamma_{jk}}x_{j})}{\sum_{j=1}^{N}{\gamma_{jk}}}, k=1,2,...,K$$
    
    $$\Sigma_{k} = \frac{\sum_{j=1}^{N}{\gamma_{jk}}(x_{j}-\mu_{k})(x_{j}-\mu_{k})^{T}}{\sum_{j=1}^{N}{\gamma_{jk}}}, k = 1,2,...,K$$
    
    $$\alpha_{k} = \frac{\sum_{j=1}^{N}{\gamma_{jk}}}{N}, k=1,2,...,K$$

4. 重复计算 E-step 和 M-step 直至收敛

    






#### difference
1. **K-means: hard assignment**
   in each iteration, we are absolutely certain as to which cluster the point belongs to
1. **GMM: soft assignment**
    It starts with some prior belief about how certain we are about each point's cluster assignments. As it goes on, it revises those beliefs


#### Reference
1. [difference of k-means and GMM](https://www.quora.com/What-is-the-difference-between-K-means-and-the-mixture-model-of-Gaussian)
2. [k-means shouldn't be our only choice](https://sites.northwestern.edu/msia/2016/12/08/k-means-shouldnt-be-our-only-choice/)
3. [EM algorithm, K-means, and GMM 1](https://zhuanlan.zhihu.com/p/30483076)
4. [EM algorithm, K-means, and GMM 2](https://zhuanlan.zhihu.com/p/75554749)