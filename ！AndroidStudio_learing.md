title : Android Studio 学习笔记
date  : 2017/5/24

---

Android Studio 视频教程地址：[http://ask.android-studio.org/?/explore/category-video](http://ask.android-studio.org/?/explore/category-video)

<!--more-->

# 008 Installing Android Studio On Windows

JDK（Java Developer Kit）下载地址：[http://www.cracle.com/technetwork/java/javase/downloads/index.html](http://www.cracle.com/technetwork/java/javase/downloads/index.html)<br>
Android Studio 下载地址：[http://developer.android.com/sdk/index.html](http://developer.android.com/sdk/index.html)

1. 下载安装相应的 windows 版本的 jdk

2. 环境配置：
    > JAVA_HOME 变量 -> 设置为 jdk 文件夹的地址<br>
    >
    > PATH 变量 -> 添加 jdk 文件夹下 bin 目录的地址<br>
    >（如果所有工作都在 Android Studio 完成的话可以不用配置该变量，但是如果要在命令行界面处理一些工作，就要设置好该变量）

3. 下载 windows 版本的 Android Studio 安装程序

4. 运行程序后可能弹出 "User Account Control"（用户账号控制）对话框，点击"确认"就好

5. 安装组件：必须安装的有 Android Studio，还应该安装 Android SDK、AVD（Android Virtual Device，安卓虚拟设备）以及 Intel HAXM 软件（在 Windows 中 HAXM 的安装是主安装程序的一部分，而在 Mac 中 HAXM 是独立安装的）

6. 安装位置：建议选择默认的安装位置，但是 Android SDK 应该安装在一个不同于 Android Studio 安装目录的另外的位置

7. 设置 Intel HAXM：默认设置 2GB 内存

8. 进行安装