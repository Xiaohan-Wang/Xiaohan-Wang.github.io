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
1. 实现前先思考代码的整体框架和结构、各部分功能，可以用xmind做一个简单思维导图
2. 尽量解耦代码，从而获得更高的复用性
    * 实现一个基础整体框架 e.g. [link](https://github.com/MrGemy95/Tensorflow-Project-Template)
    * 单独实现各个模块
    * 组合代码，同时添加一些单独的细节部分
    
##### tricks
1. 分离代码和数据
    * 最好假设它们不在一个文件夹
2. 试验参数
    * 尽量使用config文件传入，并且config尽量与log文件同名保存。
3. **train, val, test set各自的数据最好放在各自的文件夹中**


#### 实验管理
1. 使用[MLflow](https://mlflow.org/docs/latest/index.html)

#### 实验记录
1. 内容
    * 记录每个实验的目的、方法、结果
    * 尽量附代码 （用代码的 commit id）、数据
2. 工具
    * 最好用overleaf，可以与github repo 或者本地 git repo 同步 【TODO】
