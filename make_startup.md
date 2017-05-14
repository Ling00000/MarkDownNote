title : 如何使用 U 盘制作系统启动盘
date  : 2017/5/13

---

今天在教六烧了一个操作系统，痛彻心扉，决定写一篇笔记。

<!--more-->

# 所需软件
1. ultriso，下载地址[官方网站](https://cn.ultraiso.net/)
2. 操作系统 ISO 镜像包，这是使用 WIN10 专业版镜像包。

# 制作步骤
## 准备工作：
1. 插入 U 盘
2. 在制作之前需安装好 ultriso 软件，选择菜单 File -> Open.. 打开下载好的操作系统 ISO 镜像包，这里我使用 SW_DVD5_Win_Pro_10_1607_64BIT_ChnSimp_MLF_X21-07252.iso。

## 烧录系统 
1. 选择菜单 Bootable -> Write Disk Image... 打开烧录界面
2. 此时可能管理员权限
3. 在烧录界面中的 **Disk Drive** 选择烧录使用的 U 盘
4. 点击 Write 按钮即可。

## 安装操作系统
烧录完毕，拔出 U 盘插入需安装系统的电脑开机选择 U 盘启动即可。