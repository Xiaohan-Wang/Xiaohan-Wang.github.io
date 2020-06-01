---
layout:     post
title: 代码管理、实验管理
subtitle:   
date:       2020-5-15
author:     Xiaohan
header-img: img/ice.jpg
catalog: true
tags:
    - Q & A
---

目前对代码管理以及实验管理的一些小想法，部分来自[知乎](https://www.zhihu.com/question/269707221)，随时修改...

#### 项目代码
##### before starting
1. [x] 完成自己的代码框架，注意解耦代码
2. [ ] 不同项目大部分可以复用框架，另外根据具体项目添加一些细节
3. [ ] 不要盲写代码，先去github上看看是不是已经被实现了
    
##### tricks
1. 文件管理
    1. 分离代码和数据，比如说分两个文件夹data和code
    2. train, val, test set各自的数据最好放在各自的文件夹中
2. 参数管理
    1. 对于某个位置有多个选择，比如说loss可以用basic cross entropy loss，focal loss等等，用config传入选项，这样可以保存试验参数


#### 实验管理
1. 使用[MLflow](https://mlflow.org/docs/latest/index.html)

#### 实验记录
1. 内容
    * 记录每个实验的目的、方法、结果
    * 尽量附代码 （用代码的 commit id）、数据
2. 工具
    * [ ] 最好用overleaf，可以与github repo 或者本地 git repo 同步
