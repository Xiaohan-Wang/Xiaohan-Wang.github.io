---
layout:     post
title:      Unbiased Look at Dataset Bias
subtitle:   CVPR 2011
date:       2020-01-05
author:     Xiaohan
header-img: img/ice.jpg
catalog: true
tags:
    - Domain Adaptation
---

### Promise and Perils of Visual Dataset
#### Promise
1. Dataset是CV取得progress的重要因素（甚至超过算法的影响）

2. 让CV更像一门实验科学（rather than a black art）  

#### Perils
1. (good finetune + bad approach) 表现好于 (bad finetune + good approach) => 难以决定new approach的真正表现

2. pay too much attention on "winning" a competition, 但其实提高可能很微小 => 我们应该将performance number作为一个check，而不是competiton，从而给new approach留出发展的机会

### The rise of modern dataset 
repeat: one dataset -> being rejected due to its perceived biases -> new dataset -> being rejected due to its perceived biases -> ...

### Dataset Biases
Instead of representing the visual world, datasets have become closed world onto themselves.
#### selection bias
datasets often prefer particular kinds of images (e.g. street scenes, or nature scenes, or images retrieved via Internet keyword searches)
#### capture bias
photographers tending to take pictures of objects in similar ways (although this bias might be similar across the different datasets)
#### category or label bias
This comes from the fact that semantic categories are often poorly defined, and different labellers may assign differing labels to the same type of object2. 
#### <font color="#0000dd">negative set bias</font>
Datasets define a visual phenomenon (e.g. object, scene, event) not just by what it is (positive instances), but also by what it is not (negative instances). The negative set defines what the dataset considers to be “the rest of the world”. If that set is not representative, or unbalanced, that could produce classifiers that are overconfident and not very discriminative.   
><font size="3">This is particularly important for classification tasks, where the number of negatives is only a few orders of magnitude larger than the number of positives for each class. For example, if we want to find all images of “boats” in a PASCAL VOC-like classification task setting, how can we make sure that the classifier focuses on the boat itself, and not on the water below, or shore in the distance (after all, all boats are depicted in water)? This is where a large negative set (including rivers, lakes, sea, etc, without boats) is imperative to “push” the lazy classifier into doing the right thing.</font>

### Dataset value
![-w842](/img/15783472481154.jpg)

### Ways to avoid biases during dataset construction
[paper link](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=5995347&tag=1)