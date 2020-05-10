---
layout:     post
title:  为什么现在的CNN模型都是在VGGNet或者ResNet上调整的？
subtitle:   
date:       2020-5-10
author:     Xiaohan
header-img: img/ice.jpg
catalog: true
tags:
    - Q & A
---

答案来自[知乎](https://www.zhihu.com/question/43370067/answer/128881262)

Q: 为什么现在的CNN模型都是在VGGNet或者ResNet上调整的？

A:
1. 公开的论文需要一个标准的baseline及在baseline上改进的比较，因此大家会基于一个公认的baseline开始做实验，这样大家才比较信服。
2. 视觉、自然语言等更专注于本领域的内部知识，而非baseline本身。因此常常是在一个base网络的基础之上进行修改，以验证自己方法的有效性。
3. 进行基本模型的改进需要大量的实验和尝试，很有可能投入产出比比较小。对于深度学习，很大部分可以提升性能的点在于一些对于细节的精确把握。因此可以看到许多排名靠前的队伍最后讲的关键技术点似乎都是tricks。而这样精确细节的把握是需要大量的时间和计算资源的，往往在学校不可行。
4. AlexNet, Network in Network, VGG, GoogLeNet, Resnet等CNN网络都是图片分类网络, 都是在imagenet上1.2 million数据训练出来的。一般来说，某CNN网络在imagenet上面的分类结果越好，其deep feature的generalization能力越强，可以应用到各种CV问题。
