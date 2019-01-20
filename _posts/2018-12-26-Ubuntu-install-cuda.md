---
layout: post                                                    
title:  "Ubuntu安装cuda"
categories: Linux
tags: Linux Cuda
author: Tree 
---  

* content                                                       
{:toc}

1. 重启系统，别登录
2. `ctrl`+`alt`+`F3`切换到字符模式
3. `systemctl isolate multi-user.target`
4. `systemctl stop systemd-logind`
5. `modprobe -r nvidia-drm`
6. 安装cuda
7. 配置环境变量`vim ~/.bashrc`，末尾添加
```
export CUDA_HOME=/usr/local/cuda
export LD_LIBRARY_PATH=${CUDA_HOME}/lib64 
export  PATH=${CUDA_HOME}/bin:${PATH}
```
8. reboot