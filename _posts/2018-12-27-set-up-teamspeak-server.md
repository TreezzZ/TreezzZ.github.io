---
layout: post                                                    
title:  "架设TeamSpeak3服务器"
categories: Linux
tags: Linux TeamSpeak Game
author: Tree
---

* content                                                       
{:toc}

1. `wget http://dl.4players.de/ts/releases/3.1.2/teamspeak3-server_linux_amd64-3.1.2.tar.bz2` 下载服务器程序，可从官网找到最新版本的下载。
2. `tar -xvf teamspeak3-server_linux_amd64-3.1.2.tar.bz2` 解压
3. `touch .ts3server_license_accepted` 进入目录创建文件代表同意许可协议
4. `sudo adduser teamspeak` 创建teamspeak用户
5. `sudo mv teamspeak3-server_linux_amd64 /usr/local/teamspeak` 移动到新位置
6. `sudo chown -R teamspeak:teamspeak /usr/local/teamspeak` 改变用户组
7. `sudo ln -s /usr/local/teamspeak/ts3server_startscript.sh /etc/init.d/teamspeak sudo update-rc.d teamspeak defaults` 开机自启
8. `sudo service teamspeak start` 启动服务