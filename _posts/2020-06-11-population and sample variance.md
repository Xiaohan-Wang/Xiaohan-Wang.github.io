---
layout:     post
title: 从 总体 & 样本 估计总体方差
subtitle:   
date:       2020-6-11
author:     Xiaohan
header-img: img/ice.jpg
catalog: true
tags:
    - Statistics
---

#### 用总体估计总体方差
* calculating population variance and std for the whole population using all the data
* e.g. What is the standard deviation of last year’s returns of the 12 funds I have invested in? In this case, we have the data for the whole population available.
* When using the whole population to calculate population variance, **divide** the sum of squared deviations from the mean **by the number of items in the population**.

#### 用样本估计总体方差
* calculating population variance and std using only a sample of data
* e.g. What is the standard deviation of last year’s returns of equity funds in the world? In this case, we don’t have all the data available and we will have to estimate the population’s standard deviation from a sample.
* When using a sample to calculate population variance, **divide it by the number of items in the sample less one**. 
* As a result, the calculated variance (and therefore also the standard deviation) will **be slightly higher than if we would have used the population variance formula**. The purpose of this little difference is to get a better and unbiased estimate of the population‘s variance (by dividing by the sample size lowered by one, we **compensate for the fact that we are working only with a sample rather than with the whole population**).


#### 参考资料
1. https://www.macroption.com/population-sample-variance-standard-deviation/