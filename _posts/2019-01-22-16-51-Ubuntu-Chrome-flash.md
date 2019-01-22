---
layout: post                                                    
title:  "Ubuntu Chrome安装启用flash"
categories: Linux
tags: Ubuntu Chrome Flash
author: Tree 
---  

* content                                                  
{:toc}

1. `https://get.adobe.com/cn/flashplayer/otherversions/`选择对应的版本下载，Chrome选择PPAPI版本的，不要选择For Ubuntu的，下载很慢。
2. 解压下载下来的文件
3. 在Chrome安装目录下(默认`/opt/google/chrome/`)，新建文件夹`PepperFlash`
4. 将解压的文件放入`PepperFlash`中
5. `sudo vim /usr/share/applications/google-chrome.desktop`，在108行`Exec=/usr/bin/google-chrome-stable %U`后添加` --ppapi-flash-path=/opt/google/chrome/PepperFlash/libpepflashplayer.so`。注意最开始有个空格
6. 重启Chrome即可