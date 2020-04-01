---
layout:     post
title: Boosting Domain Adaptation by Discovering Latent Domains
subtitle: CVPR 2018
date:       2020-03-29
author:     Xiaohan
header-img: img/ice.jpg
catalog: true
tags: 
    - Domain Adaptation
---

[Paper link](https://research.mapillary.com/img/publications/CVPR18b.pdf) and [code](https://github.com/mancinimassimiliano/latent_domains_DA)

[//]: #(<img src="" width="40%" height="40%">)

#### Model
<img src="/img/15854715937974.jpg" width="40%" height="60%">
第一篇针对classification task的deep learning based multi-source domain adaptation. 本质上是multi-source的AdaBN.

![-w763](/img/15857203223787.jpg)
1. a side-output branch is empolyed to predict domain assignment probabilities for each input sample.
2. mDA-layer to renormalize the multi-modal feature distributions

##### domain discovery
1. domain prediction branch: sample points at different mDA-layers corresponding to a single input element to the network should share the same probabilities
2. split the network into a domain prediction branch and classification branch at some low level layer: features tend to become increasingly more domain invariant going deeper into the network, meaning that it becomes increasingly harder to compute a sample’s domain as a function of deeper features.

#####  multi-source domain adaptation layer 
> Domain Alignment layers: aim to reduce internal domain shift at different levels within the network by re-normalizing features in a domain-dependent way, matching their distributions to a pre-determined one.   

$q_{d|x}(d | x_i)$ is the conditional probability of $x_i$ belonging to $d$, given $x_i$
1. compute $\mu$ and $\sigma^2$  
    <img src="/img/15857223593758.jpg" width="30%" height="40%">  
    <img src="/img/15857224509940.jpg" width="45%" height="40%">
2. normalize each sample  
By substituting $w_{i,d}$ for $q_{d|x}(d | x_i)$  
<img src="/img/15857225154947.jpg" width="45%" height="40%">  

##### overall training objective 
only use source dataset now
<img src="/img/15857216573544.jpg" width="45%" height="40%">
1. labeled data的分类loss (cross entropy)
2. data with known domain的预测loss (cross entropy) 
3. unlabeled data的分类 (minimizing uncertainty)
4. data without domain label的预测loss (minimizing uncertainty)


#### Result
<img src="/img/15857232316372.jpg" width="50%" height="60%">
<img src="/img/15857232406316.jpg" width="50%" height="60%">
在latent domain明显的时候(digit和PACS), model表现更好。但对于office-31, 可能因为很难直接发现latent domain，所以基本没有提高。

#### Reflection
1. multi-source DA可以地方可以借鉴single-source的思想，比如说本文用的domain-alignment layer
2. 难点在于 好的latent domain discovery

#### Further reference (for latent domain discovery)
1. J. Hoffman, B. Kulis, T. Darrell, and K. Saenko. Discovering latent domains for multisource domain adaptation. In ECCV, 2012.
2. B. Gong, K. Grauman, and F. Sha. Reshaping visual datasets for domain adaptation. In NIPS, 2013.
3. C. Xiong, S. McCloskey, S.-H. Hsieh, and J. J. Corso. Latent domains modeling for visual domain adaptation. In AAAI, 2014.


