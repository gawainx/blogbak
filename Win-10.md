title: 用diskpart打造Win 10安装U盘
date: 2015-11-27 17:54:26
tags: Win10
categories: Windows
description: 用命令提示符和Windows10安装镜像制作可以在GPT+UEFI环境下引导的安装U盘
---
# 前言
本文主要介绍通过diskpart命令行的方式制作Windows10引导U盘，制作完毕后，该U盘可以用于安装（包括全新安装和升级安装）Windows10操作系统，也可以在系统无法启动的时候使用该U盘进行修复操作。
<!--more-->
# 正文
## 需要的材料
1. Windows 10 Build 10586 安装镜像。（推荐从[北邮人BT](http://bt.byr.cn)或者[IT之家](http://www.ithome.com)搜索相关的镜像。另外32位或者64位的系统镜像均适用本教程。）
2. 容量大于4GB的U盘一个。建议适用USB3.0的U盘以获得较快的安装速度。请提前备份好用户数据。
3. 以管理员账号登录当前系统。
## 制作步骤
1. 启动当前系统进入桌面环境之后，将U盘插入电脑。在开始菜单中搜索`cmd`或`命令提示符`，并右键，选择`以管理员身份运行`。
2. 在命令提示符窗口中输入`diskpart`，按回车。
3. 弹出的UAC窗口中选择`允许`，进入diskpart程序。
4. 在Diskpart程序中，输入`list disk`查看当前的磁盘列表。
5. 根据容量查看自己的U盘对应的磁盘号。这里假定第一个磁盘为你的U盘。输入`select disk 1`选中你的U盘。
6. 输入`clean`，清除U盘内容。
7. 输入`create part primary`，用于在U盘中创建主分区。大小为U盘的容量大小。
8. 输入`format`，格式化刚刚创建好的磁盘分区。磁盘格式默认是FAT32。
9. 输入`active`，激活主分区。**这步非常重要，如果忘记输入这条命令，制作的U盘将无法激活**。
10. 输入`exit`，退出程序。
11. 用文件管理器打开下载好的Win10安装ISO镜像文件，将里面的内容**全部**复制到U盘中。
12. 至此，一个可以在目前绝大部分新的笔记本电脑上启动的Windows10启动U盘已经制作完毕。在BIOS中选择用U盘启动即可进入亲切的Windows10安装界面了。
# 后记
虽然目前有很多工具可以制作启动U盘，但本文介绍的方式具有独特的优势，在你想更换别的版本的系统比如制作ubuntu启动盘（逃 的时候，只需要把U盘里面的内容全选删除，并且把ubuntu安装镜像的内容完整复制过去就可以了，不用借助任何其他工具再次制作。