---
layout:     post
title:      Pixel-Level Domain Transfer
subtitle:   ECCV 2016
date:       2020-01-07
author:     Xiaohan
header-img: img/post-bg-2015.jpg
catalog: true
tags:
    - Domain Adaptation
---
### Idea
transfer images in one domain into another domain

### Model
![-w744](/img/15784545847019.jpg)
* real/fake discriminator: 判断图像是否来自target domain
![-w727](/img/15784548684906.jpg)
* domain (semantic) discriminator: 判断是否和source domain图像具有相同semantic information
![-w729](/img/15784548946537.jpg)
* converter
 ![-w709](/img/15784556404369.jpg)

### Algorithm
![-w771](/img/15784549145475.jpg)


### Reflection
1. 作者构建的dataset将source domain和target domain中的图像make pair，从而学习image transfer。但general的DA任务并不会有source和target的image pair，因此很难直接使用  

2. MSE和discriminator：
    * MSE容易产生blurry images, 因为其假设pixels服从Gaussian distribution
    * MSE never allow a small geometric miss-alignment
    * 当有关联，但又不容易用公式描述时，可以尝试discriminator
