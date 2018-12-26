---
layout: post                                                    
title:  "Ubuntu安装pytorch docker"
categories: Pytorch
tags: Linux Pytorch Docker
author: Tree 
---  

* content                                                       
{:toc}

1. 安装docker 参考https://mirrors.tuna.tsinghua.edu.cn/help/docker-ce/
先删除以前安装过的docker 
`sudo apt-get remove docker docker-engine docker.io`
安装依赖
 `sudo apt-get install apt-transport-https ca-certificates curl gnupg2 software-properties-common`
信任Docker GPG公钥 
`curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -`
添加仓库
 `sudo add-apt-repository \
   "deb [arch=amd64] https://mirrors.tuna.tsinghua.edu.cn/docker-ce/linux/ubuntu \
   $(lsb_release -cs) \
   stable"`
安装
`sudo apt-get update
 sudo apt-get install docker-ce`
2. 安装nvidia驱动，cuda，cudnn，一定要对应好版本。出错就`sudo apt-get purge nvidia*`，清空再安装
3. 安装nvidia-docker
删除以前安装的nvidia-docker
`docker volume ls -q -f driver=nvidia-docker | xargs -r -I{} -n1 docker ps -q -a -f volume={} | xargs -r docker rm -f
sudo apt-get purge -y nvidia-docker`
添加仓库
`curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | \
  sudo apt-key add -
distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | \
  sudo tee /etc/apt/sources.list.d/nvidia-docker.list
sudo apt-get update`
安装nvidia-docker，重新加载docker
`sudo apt-get install -y nvidia-docker2
sudo pkill -SIGHUP dockerd`
4.安装pytorch docker
使用floydhub/pytorch的版本，官方的版本没有jupyter notebook，安装后中文乱码需要解决，jupyter kernel也有问题，反正各种小问题，用floydhub的就完事了，但是注意这个版本要求cuda>=9.1，cuda9.1好像是针对专门的显卡驱动开发的，折腾半天，用cuda9.2就完事了
`sudo nvidia-docker pull floydhub/pytorch:0.4.1-gpu.cuda9cudnn7-py3.35
sudo nvidia-docker run -d --network=host --name=pytorch_0.4.1 floydhub/pytorch:0.4.1-gpu.cuda9cudnn7-py3.35`
然后另开一个终端设置下jupyter notebook的密码
`sudo nvidia-docker exec -it pytorch_0.4.1 /bin/bash`
进去后`jupyter notebook password`设置密码。完毕。