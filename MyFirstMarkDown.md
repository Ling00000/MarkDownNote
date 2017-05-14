title : MarkDown 语法学习
date  : 2017/5/10

---

# 区块元素

## 段落和换行

一个 Markdown 段落是由一个或多个连续的文本行组成，它的前后要有一个以上的空行。空行的定义是显示上看起来像是空的。

## 标题

Markdown 支持两种标题的语法，类 Setext 和类 atx 形式。

类 Setext 形式是用底线的形式，利用 `=` （最高阶标题）和 `-` （第二阶标题），例如：

    This is an H1
    =========

    This is an H2
    ---------

显示如下：

This is an H1
=========

This is an H2
---------

## 区块引用

## 列表

## 代码区块

## 分割线

# 区段元素

## 链接

## 强调

## 代码

## 图片

# 其他

## 兼容HTML

不在 Markdown 涵盖范围之内的标签，都可以直接在文档里面用 HTML 撰写。
6e
要制约的只有一些 HTML 区块元素――比如 `<div>`、`<table>`、`<pre>`、`<p>` 等标签，必须在前后加上空行与其它内容区隔开，还要求它们的开始标签与结尾标签不能用制表符或空格来缩进。

Markdown 语法在 HTML 区块标签间是不会被处理的，而在 HTML 区段标签间是有效的。

## 特殊字符自动转换

在 HTML 文件中，`<` 和 `&` 两个字符需要特殊处理，而在 Markdown 中会进行自动转换。不过在代码范围内，`<` 和 `&` 两个符号会转化为 HTML 实体。

## 反斜杠

## 自动链接

# 卓建欢好帅

## 卓建欢非常帅 

### 都是他自认为的哦哈哈

>卓建欢
>想知道他
>自己为什么
>
> __那__ 么**帅**

>其实都是
他自己
*想多了*

>卓建欢说傻逼是会传染的
>>所以他女朋友也是傻逼

>##卓建欢你好
>
>bal *a* bala

* 傻逼
* 白痴
* 笨蛋

1.  A

    abc
    >引用

        代码
6. B
3. C

4\. D

这是一个普通段落：

    这是一个代码区块。
        代码区块
    代码区块
* * *
***
---
————————

This is [baidu](http://www.baidu.com) inline link.

See my [About](/about/) page for details.

This  is [an example] [id] reference-style link.

[id]:  http://example.com/ "Optional Title Here"

Use the `printf()` function.

``There is a literal backtick(`) here.``

A single backtick in a code span:`` ` ``

A backtick-delimited string in a code span:`` `foo` ``

Please don't use any `<blink>` tags.

`&#8212:` is the decimal-encoded equivalent of `&mdash:` .

![Alt text](/path/to/img.jpg)

<http://example.com/>

<address@example.com>

\*literal assterisks\*


