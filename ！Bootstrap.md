title : Bootstrap 学习笔记
date  : 2017/8/2

---

# 第 1 章 Bootstrap 介绍

## 一、Bootstrap 概述

Bootstrap 是一个基于 HTML、CSS、JavaScript 的开源框架。该框架代码简洁、视觉优美，可用于快速、简单地构建基于 PC 及移动端设备的 Web 页面需求。

Bootstrap 下载及演示：<br>
国内文档翻译官网：[http://www.bootcss.com](http://www.bootcss.com)

## 二、Bootstrap 特点

1. 跨设备、跨浏览器：兼容所有的现代浏览器

2. 响应式布局：支持 PC 端各种分辨率的显示和移动端 PAD、手机等屏幕的响应式切换显示

3. 全面的组件：提供包括导航、标签、工具条、按钮等一系列实用性很强的组件供调用

4. 内置 jQuery 插件：实现 Web 中各种常规特效

5. 支持 HTML5、CSS3

6. 支持 LESS 动态样式：LESS 使用变量、嵌套、操作混合编码，可以编写更快、更灵活的 CSS 

## 三、Bootstrap 结构

Bootstrap 下载地址：[http://v3.bootcss.com](http://v3.bootcss.com) (选择生产环境即可，v3.3.4版本)

下载解压后可看到三大核心目录：css（样式）、js（脚本）、fonts（字体）。

## 四、创建第一个页面

创建一个 HTML5 的页面，并且将 Bootstrap 的核心文件引入，测试是否正常显示。

``` html
<!-- 第一个 Bootstrap -->
<!DOCTYPE html>
<html lang="zh-cn">
<head>
    <meta charset="UTF-8">
    <title> Bootstrap 介绍</title>
    <link rel="stylesheet" href="css/bootstrap.min.css">
</head>
<body>
    <button class="btn btn-info">Bootstrap</button>
    <script src="js/jquery.min.js"></script>
    <srcipt src="js/bootstrap.min.js"></srcipt>
</body>
</html>
```

## 五、学习的各项准备

1. 开发工具：使用 Sublime Text3 作为开发工具并且安装了 Emmet 代码生成插件，我使用的是 Visual Studio Code 作为开发工具；

2. 测试工具：除了常规的浏览器，还需要移动端的测试工具，可以使用 Opera Mobile Emulator，或者 Chrome 的移动 Web 测试工具；

# 第 2 章 排版样式

Bootstrap 全局 CSS 样式中的排版样式，包括了标题、页面主体、对齐、列表等常规内容。 Bootstrap 提供了一些常规设计好的页面排版的样式供开发者使用。

## 1. 页面主体

Bootstrap 将全局 `font-size` 设置为 14px，`line-height` 行高设置为 20px；`<p>` 段落元素被设置为 10px，即 1/2 行高；颜色被设置为 #333深灰色。

## 2. 标题

Bootstrap 分别对 h1~h6 进行了 CSS 样式的重构，并且还支持普通内联元素定义 class





