---
layout:     post
title: Semantic Segmentation 
subtitle:   
date:       2020-04-21
author:     Xiaohan
header-img: img/ice.jpg
catalog: true
tags:
    - Datasets
---

部分内容来自于 https://blog.csdn.net/MOU_IT/article/details/82225505

#### 总述
目前学术界主要有三个benchmark（数据集）用于模型训练和测试。
1. Pascal VOC系列
    * VOC 2012 (最常见)
    * Pascal Context (偶尔)
    
1. Microsoft COCO  
    COCO一共有80个类别。虽然有很详细的像素级别的标注，但由于官方没有专门对语义分割的测评，因此COCO数据集往往被当成是额外的训练数据集用于模型的训练（预训练？）。
    
3. Cityscapes
    * 辅助驾驶（自动驾驶）环境
    * 使用比较常见的19个类别用于评测

#### VOC 2012

标准的VOC2012数据集有21个类别(包括背景)，包含:{ 0=background，1=aeroplane, 2=bicycle, 3=bird, 4=boat, 5=bottle, 6=bus, 7=car , 8=cat, 9=chair, 10=cow, 11=diningtable, 12=dog, 13=horse, 14=motorbike, 15=person, 16=potted plant, 17=sheep, 18=sofa, 19=train, 20=tv/monitor，255= 'void' or unlabelled }这些比较常见的类别。

对于分割任务：
1. VOC 2012用于分割的数据中train+val包含 2007-2011年间的所有数据，test包含2008-2011年间的数据，没有包含07年的是因为07年的test数据已经公开了。
2. trainval：2913张图片，共6929个物体

补充：[PASCAL VOC详细介绍](https://arleyzhang.github.io/articles/1dc20586/)

#### MS COCO
1. 官方没有semantic segmentation测评，因此该数据集常常只用于预训练
2. 数据集大小？

#### Cityscapes

补充: [Cityscapes详细介绍](https://niecongchong.github.io/2019/08/10/CityScapes%E6%95%B0%E6%8D%AE%E9%9B%86%E7%AE%80%E4%BB%8B%E4%B8%8E%E6%95%B0%E6%8D%AE%E5%A4%84%E7%90%86%E5%92%8C%E7%B2%BE%E5%BA%A6%E6%8C%87%E6%A0%87/)

1. 包含来自50个不同城市的街道场景（主要在德国）
2. 从27个城市中选择了5000张图像进行dense pixel-level annotation，其余23个城市提供了20000张有coarse annotation的图像
3. annotation包括
    * pixel-level annotation
    * instance-level labels for humans and vehicles
4. 定义了8个大类(category)，下分为30个小类(class)
    * void代表unclear (void类会在training和evaluation过程中被忽略)
    * evaluation过程中，会忽略太不常见的classes，即剩余19个classes
    ![-w721](/img/15875266001958.jpg)
5. densely annotated images被分为training, validation和test sets, 而coarsely annotated images 只作为额外的training data
    * a city is completely within a single split
    * densely annotated images中：2975 training, 500 validation images, and 1525 test images
    * 每张图片大小都是1024x2048
    ![-w878](/img/15903541919594.jpg)
6. 评价指标：
    * Pixel-Level Semantic Labelling
        * $IoU_{category}和IoU_{class}$
        * $iIoU_{category}和iIoU_{class}$ (instance-level intersection-over-union metric)
            * In contrast to the standard IoU measure, the contribution of each pixel is weighted by the ratio of the class’ average instance size to the size of the respective ground truth instance.
            * $iIoU$ metric treats instances of any size equally and is therefore more sensitive to errors in predicting small objects compared to the $IoU$
    * Instance-Level Semantic Labeling





    