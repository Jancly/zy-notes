---
layout: =
title: windows重装系统
date: 2018-11-20 09:35:59
toc : true
tags:
    - 学习
    - windows
---
>本片文章主要写了关于windows系统的重装的问题
<!-- more -->

## 重装系统的准备
介绍：我一般是用u盘重装系统，将大白菜，老毛桃，u大师等等制作u盘。
然后在MSDN微软的官方系统下载镜像

### bios的设置
1. 首先进入bios页面进行设置
2. 查看CSM boot 是否为Enabled
如果不是则将到security 将secure boot control 设置为disabled


## 重装系统时出现问题

1. reboot and select proper boot device r Insert boot Media in selshected boot device and press a key
开机出现这种情况，说是重新启动选择合适的设备
解决办法：把第一启动的选项设置为你安装的系统硬盘(我是把启动时的硬盘在bios找到作为第一启动)


## 电脑的磁盘的格式（gpt与mbr）
### UEFI+GPT与bios+mbr的优缺点
**UEFI+GPT最好用64位操作系统**
1、GPT能使用大于2.2T的硬盘，MBR不行。支持最大卷为18 EB（1EB=1048576TB）。

2、GPT可以支持无限个分区，微软目前的限定是128个。Linux、ubuntu、macos都能支持这种分区格式。MBR最多4个主分区，超过4个再分区只能通过逻辑分区。

3、GPT分区磁盘有备份分区表来提高分区数据结构的完整性。

4、UEFI + GPT 开机启动更快，开机时跳过外设检测，并且可以实现启动时原生分辨率，搭载固态硬盘开机时间很短，十秒左右。（没有开机硬件自检会稍微快了那么1、2秒）

5、UEFI + GPT 支持Secure Boot。通过保护预启动或预引导进程，抵御bootkit攻击，从而提高安全性。所有在开机时比Windows内核更早加载，实现内核劫持的技术，都可以称之为Bootkit。

6、UEFI BIOS 可用鼠标操作图形界面，不再是枯燥的蓝底白字的英文。（Intel提出，用于取代BIOS）。UEFI的优越特性：可操作性、安全性、兼容性、可扩展性。

[更多优缺点点击](https://blog.csdn.net/yang2716210363/article/details/78581388)
[对硬盘进行分区时，gpt与mbr的区别](https://blog.csdn.net/AinUser/article/details/78185432)