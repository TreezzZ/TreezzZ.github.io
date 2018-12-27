---
layout: post                                                    
title:  "ShadowSocks配置"
categories: Linux
tags: Linux ShadowSocks
author: Tree
---

* content                                                       
{:toc}

1. `sudo apt-get install python` 安装python
2. `sudo apt-get install python-pip` 安装pip
3. `sudo pip install shadowsocks` 安装shadowsocks
4. 配置服务端 `vim /etc/shadowsocks.json`
```
{
	"server":"服务器ip",
	"server_port":8388,
	"local_address":"127.0.0.1",
	"local_port":1080,
	"password":"密码",
	"method":"aes-256-cfb"
}
```
5. `ssserver -c /etc/shadowsocks.json -d start` 启动shadowsocks
6. 下面是在客户端操作。安装shadowsocks-qt5
```
sudo add-apt-repository ppa:hzwhuang/ss-qt5
sudo apt-get update
sudo apt-get install shadowsocks-qt5
```
7. 填好服务端信息
8. 安装chrome，下载SwitchyOmega插件
9. 菜单->更多工具->扩展程序->启用开发者模式，将插件拖入Chrome安装
10. 进入SwitchyOmega选项，点击情景模式分类下的proxy按钮，代理服务器中设置代理协议为SOCKS5，代理服务器为127.0.0.1，代理端口为1080，保存更改。PS:可在设定分类设置启用快速切换方便使用
11. 重启浏览器，启用SwitchyOmega，登录google尝试是否配置顺利