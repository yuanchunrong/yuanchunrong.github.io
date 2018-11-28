---
title: ubuntu16.04操作系统问题处理及优化
tags:
 - 技术
comments: true
---

## ubuntu磁盘内存不足

之前一直是使用的windows系统，windows系统对于开发实在不友好，于是进行了多种方法的尝试

首先是安装虚拟机，在虚拟机中放置ubuntu系统写代码，但是很快发现电脑容易卡死，一开虚拟机cpu立刻飙升，更别说在虚拟机里面开个pycharm和谷歌浏览器

于是抱着试试的态度装了ubuntu双系统，那时经验不足，总共只给ubuntu分配了50G的内容，一开始上手linux系统不熟悉，但是经过一个多月的尝试，发现我每次只会使用了ubuntu系列了，windows成为历史

可是我的电脑有1T的内存啊，ubuntu只有占用了50G，实在是太对不起电脑性能了

卸载重装系统再重新配置软件实在是麻烦，应该视为下策

方法一：（只能暂时解决问题，如果永远不再用另一个系统就有效）

目前的解决方法就是：

清空windows的一些磁盘，ubuntu以挂载的形式使用其它磁盘内存

具体实现方法：

1.打开终端，输入命令`$ locate ntfs-3g`检查ntfs-3g是否已经安装．如果没有安装则输入命令`$ sudo apt install ntfs-3g`.成功安装如下图所示：
![已安装ntfs-3g](http://ogzvyw5z8.bkt.clouddn.com/%E5%B7%B2%E5%AE%89%E8%A3%85ntfs-3g.png)
2.修复挂载错误的相应分区如：`/dev/sda10`，输入命令`$ sudo ntfsfix /dev/sda10`．
![成功挂载](http://ogzvyw5z8.bkt.clouddn.com/%E6%88%90%E5%8A%9F%E6%8C%82%E8%BD%BD.png)

参考链接：[双系统Ubuntu无法进入Windows磁盘的解决方法](http://www.xitongzhijia.net/xtjc/20160125/66233.html)

经过一段时间测试，遗憾的发现上述的方法并不适用，每次一更换为windows系统，再换回ubuntu系统，挂载的磁盘依然无法使用，而且更致命的是之前在磁盘中保存的数据就没了，没了...所以这个方法无效

## ChangeLog
- 2017-11-09 写ubuntu磁盘内存不足
- 2017-11-15 ubuntu磁盘内存不足＂方法一＂不够有效
