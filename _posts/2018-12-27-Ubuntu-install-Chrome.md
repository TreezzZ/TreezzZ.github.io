---
layout: post                                                    
title:  "Ubuntu安装Chrome"
categories: Linux
tags: Linux Chrome
author: Tree
---  

* content                                                       
{:toc}

1. `sudo wget https://repo.fdzh.org/chrome/google-chrome.list -P /etc/apt/sources.list.d/`添加源
2. `wget -q -O - https://dl.google.com/linux/linux_signing_key.pub | sudo apt-key add -`导入谷歌公钥
3. `sudo apt-get update`更新软件列表
4. `sudo apt-get install google-chrome-stable`安装Chrome