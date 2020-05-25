---
layout:     post
title: Image Preprocessing
subtitle:   
date:       2020-5-25
author:     Xiaohan
header-img: img/ice.jpg
catalog: true
tags:
    - Image Preprocessing
---

[//]: #(<img src="" width="100%" height="100%">)

原文：
1. https://medium.com/nanonets/how-to-use-deep-learning-when-you-have-limited-data-part-2-data-augmentation-c26971dc8ced
2. https://freecontent.manning.com/the-computer-vision-pipeline-part-3-image-preprocessing/
3. https://www.codecademy.com/articles/normalization

> No free lunch theorem for optimization:
> In ML project, it means that there's no single prescribed recipe that is guaranteed to work well in all situations. We must make certain assumption about the dataset and the problem we are trying to solve. 


#### why image preprocessing
1. The acquired data are usually messy and come from different sources, they need to be standardized and cleaned up.
2. We can’t write a unique algorithm for each of the condition in which an image is taken, thus, when we acquire an image, we tend to convert it into a form that allows a general algorithm to solve it.
3. It can reduce the complexity and increase the accuracy of the applied algorithm.


#### 彩色图像 / 灰度图像
1. In many objects, color isn’t necessary to recognize and interpret an image. Grayscale can be good enough for recognizing certain objects. Because color images contain more information than black and white images, they can add unnecessary complexity and take up more space in memory.
    <img src="/img/15904315018825.jpg" width="100%" height="100%">
2. In other applications, color is important to define certain objects. Like skin cancer detection which relies heavily on the skin colors (red rashes).

#### Standardize Image
##### Reason
1. If we didn't scale our input training vectors, the ranges of our distributions of feature values would likely be different for each feature, and thus the learning rate would **cause corrections in each dimension that would differ (proportionally speaking) from one another**. We might be over compensating a correction in one weight dimension while undercompensating in another.
2. In the process of training our network, we're going to be multiplying (weights) and adding to (biases) these initial inputs in order to cause activations that we then backpropogate with the gradients to train the model. We'd like in this process for each feature to have a similar range so that our **gradients don't go out of control**.

##### ways
1. Min-max normalization $\frac{\text{value}-\text{min}}{\text{max}-\text{min}}$: Guarantees all features will have the exact same scale but does not handle outliers well.  
    <img src="/img/15904331747160.jpg" width="60%" height="100%">  
    Normalizing fixed the squishing problem on the y-axis, but the x-axis is still problematic. Now if we were to compare these points, the y-axis would dominate; the y-axis can differ by 1, but the x-axis can only differ by 0.4.
2. Z-score normalization $\frac{value-mean}{std}$: Handles outliers, but does not produce normalized data with the exact same scale.  
    <img src="/img/15904332447812.jpg" width="60%" height="100%">  
    While the data still looks squished, notice that the points are now on roughly the same scale for both features — almost all points are between -2 and 2 on both the x-axis and y-axis. 


#### Data Augmentation
##### Offline / Online augmentation
1. Offline augmentation: 
    * 事先进行所有必需的图像平移工作，基本上就是增加数据集大小
    * 当数据集相对较小时，优先选择这种方法，因为会将数据集增大N倍（N=执行的转换数量）
2. Online augmentation:
    * 将图像输入机器学习模型之前，以小批量进行图像平移
    * 比较适合数据集较大时的情况，因为我们很难应付数据集爆炸性变大。相反，我们可以小批量平移输入到模型中的图像。有些机器学习框架支持在线增强，使用GPU可以加快增强速度。

##### 基本数据增强方法
1. 翻转
2. 旋转
    * 由于可能引入了图像边界之外的位置，可能会导致没有图像没有覆盖的黑色区域
    * 解决方法：填充未知区域
        * 常数、边缘、反射、对称
3. 平移
4. 裁剪
    * 从原始图像中随机采样一部分。然后我们将采样区域大小调整为原始图像大小
5. 缩放
5. 高斯噪声
    * 当神经网络试图学习可能并无用处的高频特征时（即频繁发生的无意义模式），常常会发生过拟合。具有零均值特征的高斯噪声本质上就是在所有频率上都有数据点，能有效使得高频特征失真，减弱它对模型的影响。这也意味着低频成分（通常也是我们关心的数据）也会失真，但神经网络能够通过学习忽略这部分影响。添加正确数量的噪声就能增强神经网络的学习能力。

* 1-3都是仿射变化，可以通过$2\times3$的矩阵实现
    * R: $2 \times 2$，线性变换矩阵
    * t: $2 \times 1$, 平移矩阵

##### 基于网络的数据增强方法
1. 条件式生成对抗网络






 
    
    