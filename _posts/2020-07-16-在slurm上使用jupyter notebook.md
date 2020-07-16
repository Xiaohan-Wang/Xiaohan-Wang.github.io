---
layout:     post
title: 通过SLURM上在节点上启动Jupyter Notebook
subtitle:   
date:       2020-7-16
author:     Xiaohan
header-img: img/ice.jpg
catalog: true
tags:
    - Configurations
---

原载于 [分享脚本远程登陆 Jupyter Notebook](https://zhuanlan.zhihu.com/p/65130699)

#### 服务器端
##### jupyterGPU.sh脚本
```zsh
#!/bin/bash
#SBATCH --partition compsci-gpu
#SBATCH --gres=gpu:2
#SBATCH --time 100:00:00
#SBATCH --job-name jupyterGPU

# get tunneling info
port=$(shuf -i8000-9999 -n1)
node=$(hostname -s)
user=$(whoami)
cluster=$(hostname -f | awk -F"." '{print $2}')

# 在这里添加你的服务器地址
clusterurl="xxx"

export PATH=$PATH:~/.local/bin

# print tunneling instructions jupyter-log
echo -e "
MacOS or linux terminal command to create your ssh tunnel:
ssh -N -L ${port}:${node}:${port} ${user}@${clusterurl}

 Here is the MobaXterm info:

 Forwarded port:same as remote port
 Remote server: ${node}
 Remote port: ${port}
 SSH server: ${cluster}.${clusterurl}
 SSH login: $user
 SSH port: 22

 Use a Browser on your local machine to go to:
 localhost:${port} (prefix w/ https:// if using password)

 or copy the URL from below and put there localhost after http:// so it would be something like:
 http://localhost:9499/?token=86c93ba16aaead7529a5da0e5e5a46be7ad8cfea35b2d49f
 "

# load modules or conda environments here
jupyter notebook --no-browser --port=${port} --ip=${node}
```
##### 提交jupyterGPU.sh脚本

```console
$ sbatch jupyterGPU.sh
```
##### 查看端口信息/浏览器信息    
```console
$ cat slurm.output
```

#### 本地
##### 监听对应端口
```console
$ ssh -N -L ${port}:${node}:${port} ${user}@${clusterurl}
```
##### 浏览器打开jupyter notebook
前往`https://localhost:${port}`





