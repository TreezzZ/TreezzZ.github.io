---
layout: post                                                    
title:  "Ubuntu安装Nvidia驱动"
categories: Linux
tags: Linux Nvidia 驱动 
author: Tree 
---  

* content                                                       
{:toc} 

1. 官网下载驱动
2. 修改`.sh`文件权限，添加执行权限
3. 禁用自带第三方驱动
`sudo vim /etc/modprobe.d/blacklist.conf` 末尾添加 `blacklist nouveau`
刷新`sudo update-initramfs -u`
重启
4. 不要登录桌面系统，进入tty1字符模式，禁用X桌面 `sudo service lightdm stop`
5. 运行`.sh`文件安装
6. 重启
