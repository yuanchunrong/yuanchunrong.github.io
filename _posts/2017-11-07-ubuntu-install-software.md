---
title: ubuntu16.04安装各种软件汇总
tags: 
 - 技术
comments: true
---

## markdown编辑器
### Mango
我使用的是Mango，初步试用，界面非常好看，支持常用的功能，可以导出为html或是pdf．
![Mango图片](http://ogzvyw5z8.bkt.clouddn.com/Mango.png)
安装方法：

１．从github下载适合的版本，我的是Linux　64bit，链接：[Mango](https://github.com/egrcc/Mango/blob/master/README-zh.md)
2.解压缩：tar zxvf 文件名.tar.gz
3.进入解压后的文件夹，双击mango即可使用．

缺点：文章字数太多(比如5000字以上)，编辑器用起来特别卡，输入一排文字往往需要等10秒左右才能够完全显示；但是字数少的时候不会出现这种问题．
### ReText
安装方法：
在命令行运行：`$ sudo apt install retext`

添加语法高亮：
1.在命令行运行`$ sudo apt install python-pygments`
2.在编辑>个人偏好>Markdown语法拓展中添加：`codehilite,`
![retext图片](http://ogzvyw5z8.bkt.clouddn.com/retext.png)

## Wireshark

网络流量分析工具[wireshark](https://www.wireshark.org/)

安装方法：
`$ sudo apt-add-repository ppa:wireshark-dev/stable`
`$ sudo apt-get update`
`$ sudo apt-get install wireshark`

分配权限：
添加wireshark用户组`$ sudo groupadd  wireshark`
将dumpcap更改为wireshark用户组`$ sudo chgrp wireshark /usr/bin/dumpcap`
让wireshark用户组有root权限使用dumpcap`$ sudo chmod 4755 /usr/bin/dumpcap`
将需要使用的普通用户名加入wireshark用户组，我的用户是“python”（需要根据具体用户名修改,在#前面可以找到哟）`$ sudo gpasswd -a python wireshark `

在搜索栏搜索wireshark，打开即可使用

参考链接：
[Ubuntu 16.04下安装网络流量分析工具 Wireshark](http://www.linuxidc.com/Linux/2016-08/134526.htm)
[ubuntu下安装wireshark(以及配置非root)](https://jingyan.baidu.com/article/c74d60009d992f0f6a595de6.html)

## Anaconda

[Anaconda](https://www.anaconda.com/download/)里面集成了python科学计算的第三方库

安装方法：

1.在官网[Anaconda](https://www.anaconda.com/download/)下载linux版本．
2.进入下载目录，打开终端，输入命令：`$ bash Anaconda3-5.0.1-Linux-x86_64.sh`.根据提示继续就好．
3.在命令行输入：`$ source ~/.bashrc`
4.测试：命令行输入`$ python`,如果看到下面有Anaconda就表示安装成功了．

参考链接：[Ubuntu16.04安装Anaconda](http://blog.csdn.net/gjq246/article/details/70848831)

## Navicat Premium
[Navicat Premium](https://www.navicat.com.cn/products/navicat-premium/)是一套数据库开发工具，让你从单一应用程序中同时连接 MySQL、MariaDB、SQL Server、Oracle、PostgreSQL 和 SQLite 数据库。它与 Amazon RDS、Amazon Aurora、Amazon Redshift、SQL Azure、Oracle Cloud 和 Google Cloud 等云数据库兼容。你可以快速轻松地创建、管理和维护数据库。

安装方法：

1.从[官网](https://www.navicat.com.cn/download/navicat-premium)下载linux版本(linux 64bit)
2.进入下载目录，解压tar文件：
`$ tar -zxvf navicat120_premium_cs_x64.tar.gz`
3.进入解压后的目录，运行命令`$ ./start_navicat`

打开时界面会显示为乱码，需要修改字符集，修改方法：
1.进入解压目录，打开start_navicat文件，把`export LANG="en_US.UTF-8"`修改为`export LANG="zh_CN.UTF-8"`
2.查看系统支持的字符集：`$ locale -a`,添加字符集：`$ export LANG=zh_CN．utf8`

破解方案：
第一次执行start_navicat时，会在用户主目录下生成一个名为.navicat64的隐藏文件夹.(具体到个人电脑可能名称有点差异，可以使用命令`$ ll`查看．)把这个文件夹删除，下次启动navicat会重新生成此文件，试用期会按新的时间进行计算．
```
python@ubuntu:~$ rm -rf .navicat64/
```
参考链接：
[Ubuntu Navicat for MySQL安装以及破解方案](http://blog.csdn.net/loadrunn/article/details/50886772)
[Ubuntu Navicat for MySQL安装及永久使用](http://www.linuxidc.com/Linux/2017-04/143122.htm)

## navicat-data-modeler
[navicat-data-modeler](http://www.navicat.com.cn/products/navicat-data-modeler)可以制作数据库模型图，同时可以直接生成sql代码，使用起来非常方便．

安装方法：
从[官网](http://www.navicat.com.cn/download/navicat-data-modeler)下载linux版本(linux 64bit)
其它安装步骤与Navicat Premium相同，可以参考前面的方法．

打开时界面会显示为乱码，需要修改字符集，修改方法：
进入解压目录，打开start_modeler文件，把`export LANG="en_US.UTF-8"`修改为`export LANG="zh_CN.UTF-8"`


## ChangeLog
- 2017-11-05 创建markdown编辑器
- 2017-11-22 安装Anaconda
- 2017-11-28 安装Navicat Premium
- 2017-12-12 安装navicat-data-modeler
