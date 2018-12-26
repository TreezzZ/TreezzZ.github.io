---
layout: post                                                    
title:  "pycocotools导入显示无法找到包"
categories: Pytorch
tags: Pytorch
author: Tree 
---  

* content                                                  
{:toc}

在python安装目录（conda下在.conda/envs/python）中找，`site-packages`文件夹，一般来说是在`<python-home>/lib/<python-version>/site-packages`。

新建文件`pycoco.pth`写入包路径，如`/usr/local/cocoapi/PythonAPI`