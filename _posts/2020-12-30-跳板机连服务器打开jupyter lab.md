---
layout:     post
title: 跳板机连服务器打开jupyter lab
subtitle:   
date:       2020-12-30
author:     Xiaohan
header-img: img/ice.jpg
catalog: true
tags:
    - Configurations
---

本地：

`ssh -L 5000:host_machine_ip:5000 username@jump_machine_ip`
1. ssh到跳板机
2. 通过跳板机监听内网ip为host_machine_ip（管理节点）的5000端口

-------

跳板机：
opt转到host_machine_ip（管理节点）

-------

host machine:  

`jupyter lab --port=5000 --ip=host_machine_ip`

jupyter_lab使用内网ip为host_machine_ip的5000端口