title : Android 入门
date  : 2017/5/21

---

Android 应用开发的基础，分为5个篇章，包括环境篇、控件篇、布局篇、组件篇和通用篇。

<!--more-->

# 第一章 搭建 Android 开发环境

## 环境组成介绍

1. JDK（Java Development kit）
2. Eclipse
3. Android SDK（Software Development kit）
4. ADT（Android Development Tools）

安卓开发工具下载：[http://tools.android-studio.org/index.php](http://tools.android-studio.org/index.php)

## 安装 JDK

1. 官方下载地址: [http://www.oracle.com/technetwork/java/javase/downloads/index.html](http://www.oracle.com/technetwork/java/javase/downloads/index.html)

2. 推荐下载 6.0 或以后的版本

3. jdk 安装：jdk 是 java 的开发工具；jre 是 java 运行环境，集成在jdk中




## 2-2 项目结构介绍
src：存放 java 源代码

gen：存放系统自动生成的配置文件

Android...：存放类库和 jar 包等

asssets：存放资源文件（音频文件，xml文件，图片等），不会自动生成 id 且不会自动占用空间

bin：存放应用被编译后生成的可指定文件（.apk）

res：存放应用用到的所有资源，如图片布局等，与 asssets 下的文件比是会占用资源的；

drawable...：存放不同密度的图片资源

layout：存放布局文件（.xml）

values...：存放字符串，主题，颜色，样式等资源文件（.xml）

AndroidManifest.xml：清单文件，配置一些与应用有关的重要信息，包含包名，权限程序组件等等


# 第3章 在界面中显示以及输入文本信息

##  3-1 控件概述

TextView：显示文本框控件

EditText：输入文本框

## 3-2 控件属性解析

常用属性：
android:id -> 控件的id
android:layout_width -> 控件的宽度
android:layout_height -> 控件的高度
android:text -> 文本内容
android:textSize -> 文本大小
android:textColor -> 文本颜色
android:background -> 控件背景
android:hint -> 输入提示文本（EditText）
android:inputType -> 输入文本类型（EditText）

## 3-3 使用 TextView 与 EditText

wrap_content：包裹实际文本内容
match_parent，fill_parent：当前控件铺满父类容器











## BUG

### Eclipse 下安卓图形设计界面使用 EditText 输入文本框错误
报错：
>Exception raised during rendering: java.lang.System.arraycopy([CI[CII)V
>
>Exception details are logged in Window > Show View > Error Log



参考网站：[http://stackoverflow.com/questions/24501042/android-app-in-eclipse-edit-text-not-showing-on-graphical-layout](http://stackoverflow.com/questions/24501042/android-app-in-eclipse-edit-text-not-showing-on-graphical-layout)