---
layout: post                                                    
title:  "Ubuntu安装JDK"
categories: Linux
tags: Linux Java
author: Tree
---

* content                                                       
{:toc}

1. 官网下载jdk安装包
2. `tar -zxvf <install-package>` 解压安装包
3. 把解压后的文件移动到想要放置的位置 比如`/usr/local/`下
4. 配置.bashrc文件
```
# config java environment 
JAVA_HOME=/usr/local/jdk10 
JRE_HOME=$JAVA_HOME/jre JAVA_BIN=$JAVA_HOME/bin 
CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin 
export JAVA_HOME JRE_HOME PATH CLASSPATH 
```
5. `source ~/.bashrc` 重新载入环境变量
6. 如果系统本来有openJDK，需要替换掉。<br />
先用`update-alternatives --config java`查看默认的java的优先级，然后修改自己的jdk为更高的优先级 <br />
`sudo update-alternatives --install /usr/bin/java java /usr/local/jdk10/bin/java 1100` <br />
`sudo update-alternatives --install /usr/bin/javac javac /usr/local/jdk10/bin/javac 1100`