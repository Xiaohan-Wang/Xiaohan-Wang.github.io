---
layout: post
title: .gitignore配置
subtitle:   
date: 2021-3-25
author:     Xiaohan
header-img: img/ice.jpg
catalog: true
tags:
    - Git
---

.gitignore简单使用

1. 前斜杠代表根目录（当前目录）
    * /data
    * /work_file
2. 后斜杠匹配文件夹以及该文件夹下的目录
    * /train/
    * /a.json
3. *通配任意多个字符；**匹配任意中间目录
    * a/**/b
    * *.png （忽略所有的png文件）
4. !表示取反（重新包含某文件），但如果之前已经排除了文件的父目录，!不起作用
   * /mtk/
   * !/mtk/one.txt
1. .gitignore 文件只能作用于Untracked Files，也就是那些从来没有被 Git 记录过的文件，如果文件曾经被 Git 记录过，那么.gitignore 就对它们完全无效
解决办法：先删除本地缓存，改为未track状态
```bash
git rm -r —cached
Git add .
Git commit -m “update .gitignore”
```
