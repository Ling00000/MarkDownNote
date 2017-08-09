title : JavaScript 基础知识
date  : 2017/5/29

---

JavaScript 入门，除了基础语法知识、数组、流程控制、函数之外的其他基础知识。

<!--more-->

# 第6章 事情响应，让网页交互

## 6-1 什么是事件

事件是可以被 JavaScript 侦测到的行为。

网页中的每个元素都可以产生某些可以触发 JavaScript 函数或程序的事件。

## 6-2 鼠标单击事件( onclick ）

onclick 是鼠标单击事件，当在网页上单击鼠标时，就会发生该事件，与此同时 onclick 事件调用的程序块就会被执行，通常与按钮一起使用。

``` html
<!DOCTYPE HTML>
<html>
    <head>
        <script type="text/javascript">
            function add2(){
                var numa,numb,sum;
                numa=6;
                numb=8;
                sum=numa+numb;
                document.write("两数和为:"+sum);  
            }
        </script>
    </head>
    <body>
        <form>
            <input name="button" type="button" value="点击提交" onclick="add2()" />
        </form>
    </body>
</html>
```

*  关于 `<!DOCTYPE HTML>`：`<!DOCTYPE>` 声明不是 HTML 标签；它是指示 web 浏览器关于页面使用哪个 HTML 版本进行编写的指令。 `<!DOCTYPE>` 必须是 HTML 文档的第一行，位于 `<html>` 标签之前。

## 6-3 鼠标经过事件（onmouseover）

鼠标经过事件，当鼠标移到一个对象上时，该对象就触发 onmouseover 事件，并执行 onmouseover 事件调用的程序。

``` html
<!DOCTYPE HTML>
<html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
        <title> 鼠标经过事件 </title>
        <script type="text/javascript">
            function message(){
                confirm("请输入密码后，再单击确定!"); 
            }
        </script>
    </head>
    <body>
        <form>
            密码:<input name="password" type="password" >
            <input name="确定" type="button" value="确定" onmouseover="message()"/>
        </form>
    </body>
</html>
```

* 关于 `<meta>` ：`<meta>` 元素可提供有关页面的元信息（ meta-information ）。`<meta>` 标签位于文档的头部，位于 `<head>` 元素内部，不包含任何内容，没有结束标签。`<meta>` 标签的属性定义了与文档相关联的名称/值对。详细参考 [http://www.w3school.com.cn/tags/tag_meta.asp](http://www.w3school.com.cn/tags/tag_meta.asp)

## 6-4 鼠标移开事件（onmouseout）

鼠标移开事件，当鼠标移开当前对象时，执行 onmouseout 调用的程序。

``` html
<!DOCTYPE HTML>
<html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
        <title>鼠标移开事件 </title>
        <script type="text/javascript">
            function message(){
                alert("不要移开，点击后进行慕课网!"); 
            }
        </script>
    </head>
    <body>
        <form>
            <a href="http://www.imooc.com" onmouseout="message()">点击我</a>
        </form>
    </body>
</html>
```

## 6-5 光标聚焦事件（onfocus）

当网页中的对象获得聚点时，执行 onfocus 调用的程序就会被执行。

``` html
<!DOCTYPE HTML>
<html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
        <title> 光标聚焦事件 </title>
        <script type="text/javascript">
            function message(){
                alert("请选择，您现在的职业！");
            }
        </script>
    </head>
    <body>
        请选择您的职业：<br>
        <form>
            <select name="career" onfocus="message()"> 
                <option>学生</option> 
                <option>教师</option> 
                <option>工程师</option> 
                <option>演员</option> 
                <option>会计</option> 
            </select> 
        </form>
    </body>
</html>
```

## 6-6 失焦事件（onblur）

onblur 事件与 onfocus 是相对事件，当光标离开当前获得聚焦对象的时候，触发 onblur 事件，同时执行被调用的程序。

``` html
<html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
        <title> 失焦事件 </title>
        <script type="text/javascript">
            function message(){
                alert("请确定已输入密码后，在移开!"); 
            }
        </script>    
    </head>
    <body>
        <form>
            用户:<input name="username" type="text" value="请输入用户名！" >
            密码:<input name="password" type="text" value="请输入密码！" onblur="message()" >
        </form>
    </body>
</html>
```

## 6-7 内容选中事件（onselect）

选中事件，当文本框或者文本域中的文字被选中时，触发 onselect 事件，同时调用的程序就会被执行。

``` html
<!DOCTYPE HTML>
<html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
        <title> 内容选中事件 </title>
        <script type="text/javascript">
            function message(){
                alert("您触发了选中事件！"); 
            }
        </script>    
    </head>
    <body>
        <form>
            个人简介：<br>
            <textarea name="summary" cols="60" rows="5" onselect="message()" >请写入个人简介，不少于200字！</textarea>
        </form>
    </body>
</html>
```

## 6-8 文本框内容改变事件（onchange）

通过改变文本框的内容来触发 onchange 事件，同时执行被调用的程序。

``` html
<!DOCTYPE HTML>
<html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
        <title> 文本框内容改变事件 </title>
        <script type="text/javascript">
            function message(){
                alert("您改变了文本内容！"); 
            }
        </script>    
    </head>
    <body>
        <form>
            个人简介：<br>
            <textarea name="summary" cols="60" rows="5" onchange="message()">请写入个人简介，不少于200字！</textarea>
        </form>
    </body>
</html>
```

## 6-9 加载事件（onload）

事件会在页面加载完成后，立即发生，同时执行被调用的程序。**注意**：
1. 加载页面时，触发 onload 事件，事件写在 `<body>` 标签内；
2. 此处的加载页面，可理解为打开一个新页面时。

``` html
<!DOCTYPE HTML>
<html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
        <title> 加载事件 </title>
        <script type="text/javascript">
            function message(){
                alert("加载中，请稍等…"); 
            }
        </script>    
    </head>
    <body onload="message()">
        欢迎学习JavaScript。
    </body>
</html>
```

## 6-10 卸载事件（onunload）

当用户退出页面时（页面关闭、页面刷新等），触发 onUnload 事件，同时执行被调用的程序。**注意**：不同浏览器对 onunload 事件支持不同。

``` html
<!DOCTYPE HTML>
<html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
        <title> 卸载事件 </title>
        <script type="text/javascript">   
            window.onunload = onunload_message;   
            function onunload_message(){   
                alert("您确定离开该网页吗？");   
            }   
        </script>   
    </head>
    <body>
        欢迎学习JavaScript。
    </body>
</html>
```

# 第7章 JavaScript 内置对象

## 7-1 什么是对象

JavaScript 中的所有事物都是对象，如:字符串、数值、数组、函数等，每个对象带有属性和方法。JavaScript 提供多个内建对象，比如 String、Date、Array 等等，使用对象前要先定义。

1. 对象的属性：反映该对象某些特定的性质的，如：字符串的长度、图像的长宽等。访问对象属性的语法: `objectName.propertyName` ，如使用 Array 对象的 length 属性来获得数组的长度：
``` html
var myarray=new Array(6);//定义数组对象
var myl=myarray.length;//访问数组长度length属性
```

2. 对象的方法：能够在对象上执行的动作。例如，表单的“提交”(Submit)，时间的“获取”(getYear)等。访问对象的方法： `objectName.methodName()` ，如使用string 对象的 toUpperCase() 方法来将文本转换为大写：
``` html
var mystr="Hello world!";//创建一个字符串
var request=mystr.toUpperCase(); //使用字符串对象方法
```

## 7-2 Date 日期对象

日期对象可以储存任意一个日期，并且可以精确到毫秒数（1/1000 秒）。

定义一个时间对象： `var Udate=new Date();`

应注意的是，使用关键字 `new` 时，`Date()` 的首字母必须大写，并且 Udate 已有初始值，即为当前时间(当前电脑系统时间)。

如果要自定义初始值，可以： `var d = new Date(2012, 10, 1);` 或者 `var d = new Date('Oct 1, 2012'); `

## 7-3 返回/设置年份方法

`get/setFullYear()` 返回/设置年份，用四位数表示。

``` js
var mydate=new Date();//当前时间
document.write(mydate+"<br>");//输出当前时间
document.write(mydate.getFullYear()+"<br>");//输出当前年份
mydate.setFullYear(81); //设置年份
document.write(mydate+"<br>"); //输出年份
```

* 注意：不同浏览器的时间格式有差异。

## 7-4 返回星期方法

`getDay(`) 返回星期，返回的是 0-6 的数字，0 表示星期天。如果要返回相对应“星期”，通过数组完成，代码如下:

``` js
var mydate=new Date();//定义日期对象
var weekday=["星期日","星期一","星期二","星期三","星期四","星期五","星期六"];//定义数组对象,给每个数组项赋值
var mynum=mydate.getDay();//返回值存储在变量mynum中
document.write("今天是："+ weekday[mynum]);//输出星期几
```

## 7-5 返回/设置时间方法

`get/setTime()` 返回/设置时间，单位毫秒数，计算从 1970 年 1 月 1 日零时到日期对象所指的日期的**毫秒**数。

``` js
var mydate=new Date();
document.write("当前时间："+mydate+"<br>");
mydate.setTime(mydate.getTime() + 60 * 60 * 1000);
document.write("推迟一小时时间：" + mydate);
```

## 7-6 String 字符串对象

``` js
var mystr = "I love JavaScript!";
var myl=mystr.length;
var myupper=mystr.toUpperCase();
var mylower=mystr.toLowerCase();
```

## 7-7 返回指定位置的字符

`charAt()` 方法可返回指定位置的字符。返回的字符是长度为 1 的字符串。

语法：`stringObject.charAt(index)`

注意：
1. 字符串中第一个字符的下标是 0 。最后一个字符的下标为 string.length-1
2. 如果参数 index 不在 0 与 string.length-1 之间，该方法将返回一个空字符串
3. 一个空格也算一个字符

``` js
var mystr="I love JavaScript!";
document.write(mystr.charAt(2));
```

## 7-8 返回指定的字符串首次出现的位置

`indexOf()` 方法可返回某个指定的字符串值在字符串中**首次**出现的位置。

语法：`stringObject.indexOf(substring, startpos)`

说明：
1. 该方法将从头到尾地检索字符串 stringObject ，看它是否含有子串 substring ，如果找到，就返回 substring 的第一次出现的位置
2. startpos 是可选参数，从 stringObject 的 startpos 位置开始查找 substring ，如果没有此参数将从 stringObject 的开始位置查找
3. stringObject 中的字符位置是从 0 开始的

注意：
1. `indexOf()` 方法区分大小写
2. 如果要检索的字符串值没有出现，则该方法返回 -1 

``` js
var str="I love JavaScript!";
document.write(str.indexOf("v")+"<br>");
document.write(str.indexOf("v",8)+"<br>");
document.write(str.indexOf("v", str.indexOf("v")+1)+"<br>");
```

## 7-9 字符串分割 split()

`split()` 方法将字符串分割为字符串数组，并返回此数组。

语法：`stringObject.split(separator,limit)`

说明：
1. separator 是必需参数，`split()` 方法从该参数指定的位置分割 stringObject 
2. limit 是可选参数，指定分割的次数，方法返回的子串不会多于这个参数指定的数组，没有这个参数的话即为不限制次数

``` js
var mystr = "www.imooc.com";
document.write(mystr.split(".")+"<br>");
document.write(mystr.split(".", 2)+"<br>");
document.write(mystr.split("")+"<br>");
document.write(mystr.split("", 5)+"<br>");
```

* 运行结果：
``` bash
www,imooc,com
www,imooc
w,w,w,.,i,m,o,o,c,.,c,o,m
w,w,w,.,i
```

## 7-10 提取字符串 substring()

`substring()` 方法用于提取字符串中介于两个指定下标之间的字符。

语法：`stringObject.substring(startPos,stopPos)`

注意：
1. 返回的内容是从 start 开始（包含 start 位置的字符）到 stop-1 处的所有字符，其长度为 stop 减 start 
2. 如果参数 start 与 stop 相等，那么该方法返回的就是一个空串（即长度为 0 的字符串）
3. 如果 start 比 stop 大，那么该方法在提取子串之前会先交换这两个参数

``` js
var mystr="I love JavaScript";
document.write(mystr.substring(7));
document.write(mystr.substring(2,6));
```

## 7-11 提取指定数目的字符 substr()

`substr()` 方法从字符串中提取从 startPos 位置开始的指定数目的字符串。

语法：`stringObject.substr(startPos,length)`

注意：如果参数 startPos 是负数，则是从字符串的尾部开始算起的位置，也就是说，-1 指字符串中最后一个字符，-2 指倒数第二个字符，以此类推。如果 startPos 为负数且绝对值大于字符串长度，startPos 为 0 。

``` js
var mystr="I love JavaScript!";
document.write(mystr.substr(7));
document.write(mystr.substr(2,4));
```

## 7-12 Math 对象

Math 对象，提供对数据的数学计算。

Math 对象是一个**固有的对象**，无需创建它，直接把 Math 作为对象使用就可以调用其所有属性和方法。这是它与 Date,String 对象的区别

## 7-13 向上取整 ceil()

`ceil()` 方法可对一个数进行向上取整。

语法：`Math.ceil(x)`

``` js
document.write(Math.ceil(3.5)+ "<br>");
document.write(Math.ceil(-5.1)+ "<br>");
```

## 7-14 向下取整 floor()

`floor()` 方法可对一个数进行向下取整。

语法：`Math.floor(x)`

``` js
document.write(Math.floor(3.5)+ "<br>");
document.write(Math.floor(-5.1)+ "<br>");
```

## 7-15 四舍五入 round()

`round()` 方法可把一个数字四舍五入为最接近的整数。

语法：`Math.round(x)`

注意：
1. 返回与 x 最接近的整数
2. 对于出现 0.5 或者 -0.5 之类的情况，即 x 与两侧整数同等接近，该方法将进行上舍入，如：5.5 将舍入为 6 ， -5.5 将舍入为 -5

``` js
document.write(Math.round(2.5)+ "<br>");
document.write(Math.round(-6.4)+ "<br>");
```

## 7-16 随机数 random()

`random()` 方法可返回介于 0~1（**大于或等于 0 但小于 1** )之间的一个随机数。

语法：`Math.random()`

``` js
document.write(Math.random()+ "<br>");//取得 0~1 之间的一个随机数
document.write((Math.random())*10+ "<br>");//获得 0~10 之间的一个随机数

//使用 random() 方法和 round() 方法，得到一个不大于10的整数
document.write(Math.round(Math.random()*10)+ "<br>");
```

## 7-17 Array 数组对象

略

## 7-18 数组连接 concat()

`concat()` 方法用于连接两个或多个数组。此方法返回一个**新数组**，不改变原来的数组。

语法：`arrayObject.concat(array1,array2,...,arrayN)`

注意：该方法不会改变现有的数组，而仅仅会返回被连接数组的一个**副本**

``` js
var mya1= new Array("hello!")
var mya2= new Array("I","love");
var mya3= new Array("JavaScript","!");
var mya4=mya1.concat(mya2,mya3);
document.write(mya4);
```

* 运行结果
``` Bash
hello!,I,love,JavaScript,!
```

## 7-19 指定分隔符连接数组元素 join()

`join()` 方法用于把数组中的所有元素放入一个字符串。元素是通过指定的分隔符进行分隔的。

语法：`arrayObject.join(分隔符)`

说明：参数 分隔符 是可选参数，可以指定要使用的分隔符，如果省略该参数则默认使用逗号作为分隔符

注意：**返回一个字符串**，该字符串把数组中的各个元素串起来，用 <分隔符> 置于元素与元素之间。这个方法不影响数组原本的内容。

``` js
var myarr = new Array(3);
myarr[0] = "I";
myarr[1] = "love";
myarr[2] = "JavaScript";
document.write(myarr.join("."));
```

* 运行结果
``` Bash
I.love.JavaScript
```

## 7-20 颠倒数组元素顺序 reverse()

`reverse()` 方法用于**颠倒**数组中元素的顺序。

语法：`arrayObject.reverse()`

注意：该方法会改变原来的数组，而**不会创建新的数组**

``` js
var myarr1= ["我","爱","你"];
document.write(myarr1.reverse());
```

## 7-21 选定元素 slice()

`slice()` 方法可从已有的数组中返回选定的元素。

语法：`arrayObject.slice(start,end)`

注意：
1. 可使用负值从数组的尾部选取元素
2. 如果 end 未被规定，那么 slice() 方法会选取从 start 到数组结尾的所有元素
3. String.slice() 与 Array.slice() 相似
2. 该方法并**不会修改数组**，而是返回一个子数组

``` js
var myarr1= ["我","爱","你"];
document.write(myarr1.slice(1));
```

## 7-22 数组排序 sort()

`sort()` 方法使数组中的元素按照一定的顺序排列。

语法：`arrayObject.sort(方法函数)`

说明：如果不指定 <方法函数> ，则按unicode码顺序排列

注意：<br>
方法函数要比较两个值，然后返回一个用于说明这两个值的相对顺序的数字。比较函数应该具有两个参数 a 和 b，其返回值如下： <br>
若返回值<=-1，则表示 A 在排序后的序列中出现在 B 之前；<br>
若返回值>-1 && <1，则表示 A 和 B 具有相同的排序顺序；<br>
若返回值>=1，则表示 A 在排序后的序列中出现在 B 之后。

``` js
function sortNum(a,b) {
    return a - b;//升序
}
var myarr = new Array("80","16","50","6","100","1");
document.write(myarr.sort() + "<br>");
document.write(myarr.sort(sortNum)+ "<br>");
```
* 运行结果
``` Bash
1,100,16,50,6,80
1,6,16,50,80,100
```

# 第8章 浏览器对象 

## *补充讲解：常用的窗口互动方法

1. `document.write()` <br>
可用于直接向 HTML 输出流写内容，简单的说就是直接在网页中输出内容。

2. `alert(str)` <br>
弹出包含一个"确定"按钮的消息对话框，在点击"确定"按钮前不能进行任何其它操作。通常可以用于调试程序（比如常见的警告窗口）。

3. `confirm(str)`<br>
弹出包含一个"确定"按钮和一个"取消"按钮的消息对话框，同样在点击对话框按钮前不能进行任何其他操作。通常用于允许用户做选择的动作。<br>
需要说明的是，`comfirm()` 返回的是一个 Boolean 值：点击"确定"按钮时返回 true ，点击"取消"按钮时返回 false ，通过返回值判断用户点击了什么按钮。

4. `prompt(str1, str2)`<br>
弹出包含一个"确定"按钮、一个"取消"按钮和一个文本输入框的消息对话框，在用户点击对话框的按钮前，不能进行任何其它操作。通常用于询问一些需要与用户交互的信息。<br>
对于参数，str1 参数是要显示在消息对话框中的文本，不可修改，str2 参数是文本框中的内容，可以修改；<br>
对于返回值，点击"确定"按钮，文本框中的内容将作为函数返回值；点击"取消"按钮，将返回 null 。

5. `window.open([URL], [name], [str])`<br>
查找一个已经存在或者新建的浏览器窗口。<br>
参数说明：
    * URL：可选参数，在窗口中要显示网页的网址或路径。如果省略这个参数，或者它的值是空字符串，那么窗口就不显示任何文档。
    * name：可选参数，被打开窗口的名称，由字母、数字和下划线字符组成，不能包含有空格。相同 name 的窗口只能创建一个，要想创建多个窗口则 name 不能相同。具有特殊意义的名称：
        * _blank ：在新窗口显示目标网页<br>
        * _self ：在当前窗口显示目标网页<br>
        * _top ：框架网页中在上部窗口中显示目标网页<br>
    * str：可选参数，设置窗口参数，各参数用逗号隔开。主要参数：
        * top，left：窗口顶部/左端离开屏幕顶部/左端的像素数，数值
        * width，height：窗口的宽度/高度，数值
        * menubar，toolbar，scrollbars，status：窗口是否有菜单/工具条/滚动条/状态栏，布尔值

    ``` js
    function Wopen(){
        window.open('http://www.imooc.com','_blank','width=300,height=200,menubar=no,toolbar=no, status=no,scrollbars=yes')
    } 
    ```

6. `window.close() 或 <窗口对象>.close()`<br>
关闭本窗口或者关闭指定的窗口。

## 8-1 window 对象

window 对象是 BOM 的核心，window 对象指当前的浏览器窗口。

## 8-2 JavaScript 计时器

在 JavaScript 中，我们可以在一个设定的时间间隔之后来执行代码，而不是在函数被调用后立即执行，我们称之为计时事件。 

计时器类型：<br>
间隔性触发计时器：每隔一定的时间间隔就触发一次<br>
一次性计时器：仅在指定的延迟时间之后触发一次

## 8-3 计时器 setInterval()

`setInterval()` 计时器，在执行时,从载入页面后**每隔指定的时间**执行代码。

语法：`setInterval(代码,交互时间)`

参数说明：<br>
代码：要调用的函数或要执行的代码串<br>
交互时间：周期性执行或调用表达式之间的时间间隔，**以毫秒计**（1s=1000ms）

返回值：<br>
一个可以传递给 `clearInterval()` 从而取消对"代码"的周期性执行的值

## 8-4 取消计时器 clearInterval()

`clearInterval()` 方法可取消由 `setInterval()` 设置的交互时间。

语法：`clearInterval(id_of_setInterval)`

参数说明：<br>
id_of_setInterval：由 `setInterval()` 返回的值

``` html
<!DOCTYPE HTML>
<html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
        <title>时钟</title>
        <script type="text/javascript">
            var attime;
            function clock(){
                var time=new Date();          
                attime= time.getHours()+":"+time.getMinutes()+":"+time.getSeconds();
                document.getElementById("clock").value = attime;
            }
            var int = setInterval(clock,1000);
        </script>
    </head>
    <body>
        <form>
            <input type="text" id="clock" size="4" />
            <input type="button" value="Stop" onclick="clearInterval(int)" />
        </form>
    </body>
</html>
```

## 8-5 计时器 setTimeout()

`setTimeout()` 计时器，在载入后延迟指定时间后,去执行一次表达式,**仅执行一次**。

语法：`setTimeout(代码,延迟时间)`

参数说明：<br>
代码：要调用的函数或要执行的代码串<br>
延时时间：在执行代码前需等待的时间，以毫秒为单位（1s=1000ms)

## 8-6 取消计时器 clearTimeout()

`setTimeout()` 和 `clearTimeout()` 一起使用，停止计时器。

语法：`clearTimeout(id_of_setTimeout)`

参数说明:<br>
id_of_setTimeout：由 `setTimeout()` 返回的值,该值标识要取消的延迟执行代码块

```html
<!DOCTYPE HTML>
<html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
        <title>计时器</title>
        <script type="text/javascript">
            var num=0;
            var i;
            function startCount(){
                document.getElementById('count').value=num;
                num=num+1;
                i=setTimeout("startCount()",1000);
            }
            function stopCount(){
                clearTimeout(i);
            }
        </script>
    </head>
    <body>
        <form>
            <input type="text" id="count" />
            <input type="button" value="Start" onclick="startCount()" />
            <input type="button" value="Stop" onclick="stopCount()" />
        </form>
    </body>
</html>
```

## 8-7 history 对象

history 对象记录了用户曾经浏览过的页面（URL），并可以实现浏览器前进与后退的相似导航功能。

从窗口被打开的那一刻就开始记录；每个浏览器窗口、每个标签页乃至每个框架，都有自己的 history 对象与特定的 window 对象关联。

## 8-8 返回前一个浏览的页面

`back()` 方法，加载 history 列表中的前一个 URL，等同于点击浏览器的倒退按钮。`back()` 相当于 `go(-1)`。

语法：`window.history.back()`（ window 前缀可以省略，下同）

## 8-9 返回下一个浏览的页面

`forward()` 方法，倒退之后再想回到倒退之前浏览的页面，即加载 history 列表中的下一个 URL，等价点击前进按钮。`forward()` 相当于 `go(1)`。

语法：`window.history.forward()`

## 8-10 返回浏览历史中的其他页面

`go()` 方法，根据当前所处的页面，加载 history 列表中的某个具体的页面。

语法：`window.history.go(number)`<br>
其中 number 表示要访问的 URL 在 history 的 URL 列表中相对于当前页面的位置。

特别的，`go(-1)` 相当于 `back()`，`go(1)` 相当于 `forward()`，`go(0)` 指向当前页面。

## 8-11 location 对象

location 对象用于获取或设置窗体的 URL ，并且可以用于解析 URL 。

语法：`window.location.[属性/方法]`（ window 前缀可以省略）


location 对象的属性：<br>
_（eg ： http://www.imooc.com:8080//list.php?courseid=8&chapterid=86#mediaid118 ）_
* `hash` ：设置并返回从 '#' 开始的 URL（锚），如 _"mediaid118"_
* `host` ：设置并返回主机名和当前 URL 的端口号，如 _"www.imooc.com:8080"_
* `hostname` ：设置并返回当前 URL 的主机名，如 _"www.imooc.com"_
* `href` ：设置并返回完整的 URL ，如 _"http://www.imooc.com:8080//list.php?courseid=8&chapterid=86#mediaid118"_
* `pathname` ：设置并返回当前 URL 的路径部分，如 _"list.php"_
* `port` ：设置并返回当前 URL 的端口号，如 _"8080"_
* `protocol` ：设置并返回当前 URL 的协议，如 _"http"_
* `search` ： 设置并返回从 '?' 开始的 URL（查询部分），如 _"courseid=8&chapterid=86"_

location 对象的方法:
* `assign()` ：加载新的文档
* `reload()` ：重新加载当前文档
* `replace()` ：用新的文档替换当前文档

## 8-12 navigator 对象

navigator 对象包含有关浏览器的信息，通常用于检测浏览器与操作系统的版本。

navigator 对象的属性：
* `appCodeName` ：浏览器代码名的字符串表示
* `appName` ：返回浏览器的名称
* `appVersion` ：返回浏览器的平台和版本信息
* `platform` ：返回运行浏览器的操作系统平台
* `userAgent` ：返回由客户机发送服务器的 user-agent 头部的值

## 8-13 userAgent

`userAgent` 属性返回用户代理头的字符串表示（就是包括浏览器版本信息等的字符）

语法：`navigator.userAgent`

``` html
<!DOCTYPE HTML>
<html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
        <title>navigator</title>
        <script type="text/javascript">
            function validB(){ 
                var u_agent = navigator.userAgent; 
                var B_name="Failed to identify the browser"; 
                if(u_agent.indexOf("Firefox")>-1){ 
                    B_name="Firefox"; 
                }else if(u_agent.indexOf("Chrome")>-1){ 
                    B_name="Chrome"; 
                }else if(u_agent.indexOf("MSIE")>-1&&u_agent.indexOf("Trident")>-1){ 
                    B_name="IE(8-10)";  
                }
                document.write("B_name:"+B_name+"<br>");
                document.write("u_agent:"+u_agent+"<br>"); 
            } 
        </script>
    </head>
    <body>
        <form>
            <input type="button" value="查看浏览器" onclick="validB()">
        </form>
    </body>
</html>
```

## 8-14 screen 对象

screen 对象用于获取用户的屏幕信息。

## 8-15 屏幕分辨率的高和宽

screen 对象的 height/width 属性：返回屏幕分辨率的高/宽，以像素计。

## 8-16 屏幕可用高和宽度

screen 对象 的 availWidth/availHeight 属性：返回访问者屏幕的宽度/高度，以像素计，减去界面特性，比如任务栏。

注意：不同系统的任务栏默认高度不一样，且任务栏的位置可在屏幕上下左右任何位置，所以有可能可用宽度和高度不一样。


# 第9章 DOM 对象，控制 HTML 元素 

## *补充讲解： DOM 基本操作

1. `document.getElementById("id") `<br>
通过 id 属性获取元素，得到的是一个对象（Object）。

2. `Object.innerHTML = new HTML`<br>
通过`innerHTML` 属性修改获取到的 HTML 元素的内容。

3. `Object.style.property = new style`<br>
通过设置 `property`（基本属性）来改变获取到的 HTML 元素的样式，如 color，backgroundColor，height，width，font 等。

4. `Object.style.display = value`<br>
通过改变 `display` 属性的 value 值来设置获取到的 HTML 元素的显示和隐藏的效果。<br>
value 值为 "none" 时，元素不会被显示，即隐藏；value 值为 "block" 元素将显示为块级元素，即显示。

5. `object.className = classname`<br>
通过 `className` 属性可以获取元素的 class 属性或更改某个元素外观为指定的 css 样式
    ``` html
    <!DOCTYPE HTML>
    <html>
        <head>
        <meta http-equiv="Content-Type" content="text/html; charset=gb2312">
            <title>className属性</title>
            <style>
                body{ font-size:16px;}
                .one{
                    border:1px solid #eee;
                    width:230px;
                    height:50px;
                    background:#ccc;
                    color:red;
                }
                .two{
                    border:1px solid #ccc;
                    width:230px;
                    height:50px;
                    background:#9CF;
                    color:blue;
                }
            </style>
        </head>
        <body>
            <p id="p1" > JavaScript使网页显示动态效果并实现与用户交互功能。</p>
                <input type="button" value="添加样式" onclick="add()"/>
            <p id="p2" class="one">JavaScript使网页显示动态效果并实现与用户交互功能。</p>
                <input type="button" value="更改外观" onclick="modify()"/>
                <script type="text/javascript">
                    function add(){
                        var p1 = document.getElementById("p1");
                        p1.className = "one";
                    }
                    function modify(){
                        var p2 = document.getElementById("p2");
                        p2.className = "two";
                    }
                </script>
        </body>
    </html>
    ```

## 9-1 认识 DOM

文档对象模型 DOM（Document Object Model）定义了访问和处理 HTML 文档的标准方法。

DOM 将 HTML 文档呈现为带有元素、属性和文本的树结构（节点树）。

HTML 文档可以说由节点构成的集合，DOM 节点有:
1. 元素节点：上图中 `<html>`、`<body>`、`<p>`等都是元素节点，即标签。
2. 文本节点：向用户展示的内容，如 `<li>` . . . `</li>` 中的 JavaScript、DOM、CSS 等文本。
3. 属性节点：元素属性，如 `<a>` 标签的链接属性 href="http://www.imooc.com" 。

## 9-2 getElementsByName() 方法

`getElementsByName()` 方法可返回带有指定名称的节点对象的集合。

语法：`document.getElementsByName(name)`

说明:
1. 因为文档中的 `name` 属性可能不唯一，所有 `getElementsByName()` 方法返回的是**元素的数组**，而不是一个元素
2. 和数组类似也有 `length` 属性，可以和访问数组一样的方法来访问，从 0 开始

## 9-3 getElementsByTagName() 方法

`getElementsByTagName()` 方法可返回带有指定标签名的节点对象的集合。返回元素的顺序是它们在文档中的顺序。

语法：`document.getElementsByTagName(Tagname)`

说明:
1. Tagname  是标签的名称，如 p、a、img 等标签名。
2. 和数组类似也有 `length` 属性，可以和访问数组一样的方法来访问，所以从 0 开始。

## 9-4 区别 getElementById，getElementsByName，getElementsByTagName

## 9-5 getAttribute() 方法

`getAttribute()` 方法可通过元素节点的属性名称获取属性的值。

语法：`elementNode.getAttribute(name)`

说明:
1. elementNode：使用getElementById()、getElementsByTagName()等方法，获取到的元素节点
2. name：要想查询的元素节点的属性名字

## 9-6 setAttribute() 方法

`setAttribute()` 方法可增加一个指定名称和值的新属性，或者把一个现有的属性设定为指定的值。

语法：`elementNode.setAttribute(name,value)`

说明：
1. name 参数为要设置的属性名；value 参数为要设置的属性值
2. 把指定的属性设置为指定的值。如果不存在具有指定名称的属性，该方法将创建一个新属性
2. 类似于 `getAttribute()` 方法，`setAttribute()` 方法只能通过元素节点对象调用的函数

## 9-7 节点属性

在文档对象模型（DOM）中，每个节点都是一个对象。DOM 节点有三个重要的属性：

1. `nodeName` 属性: 节点的名称，是只读的。
    * 元素节点的 `nodeName` 与标签名相同
    * 属性节点的 `nodeName` 是属性的名称
    * 文本节点的 `nodeName` 永远是 #text
    * 文档节点的 `nodeName` 永远是 #document

2. `nodeValue` 属性：节点的值。
    * 元素节点的 `nodeValue` 是 undefined 或 null
    * 文本节点的 `nodeValue` 是文本自身
    * 属性节点的 `nodeValue` 是属性的值

3. `nodeType` 属性: 节点的类型，是只读的。
    * 元素节点的 `nodeType` 是 1
    * 属性节点的 `nodeType` 是 2
    * 文本节点的 `nodeType` 是 3
    * 注释节点的 `nodeType` 是 8
    * 文档节点的 `nodeType` 是 9

## 9-8 访问子节点 childNodes

`childNodes` 属性可访问选定元素节点下的所有子节点的列表，返回的值可以看作是**一个数组**，他具有 `length` 属性。

语法：`elementNode.childNodes`

说明：<br>
如果选定的节点没有子节点，则该属性返回不包含节点的 NodeList。

### *补充：关于子节点的判断
``` html
代码1
<ul>
  <li>javascript</li>
  <li>jQuery</li>
  <li>PHP</li>
</ul>
```
``` html
代码2
<ul><li>javascript</li><li>jQuery</li><li>PHP</li></ul>
```
对于上面这段 代码1 中 'ul' 的子节点的判断，不同浏览器会出现不同的结果，但是对于 代码2 则不会出现不同的结果。

这是因为有的浏览器，比如 IE 浏览器，会自动过滤节点之间生成的空白文本节点，而有的浏览器则不会。

这种情况会影响到一些操作，**解决方法**是通过检测节点类型，进行子节点过滤：判断节点 `nodeType` 是否为 1，如是，则为元素节点，保留，不过滤

## 9-9 访问子节点的第一和最后项

1. `firstChild` 属性可返回 'childNodes' 数组的第一个子节点。如果选定的节点没有子节点，则该属性返回 NULL。<br><br>
语法：`node.firstChild` <br>
（与 `elementNode.childNodes[0]` 是同样的效果） 

2. `lastChild` 属性可返回 'childNodes' 数组的最后一个子节点。如果选定的节点没有子节点，则该属性返回 NULL。<br><br>
语法：`node.lastChild` <br>
（与 `elementNode.childNodes[elementNode.childNodes.length-1]` 是同样的效果） 

## 9-10 访问父节点 parentNode

`parentNode` 属性可获取指定节点的父节点。父节点只能有一个。

语法：`elementNode.parentNode`

同样的可以访问祖节点：`elementNode.parentNode.parentNode`

## 9-11 访问兄弟节点

1. `nextSibling` 属性可返回某个节点之后紧跟的节点（处于同一树层级中）。如果无此节点，则该属性返回 null。<br><br>
语法：`nodeObject.nextSibling`

2. `previousSibling` 属性可返回某个节点之前紧跟的节点（处于同一树层级中）。如果无此节点，则该属性返回 null。<br><br>
语法：`nodeObject.previousSibling`

## 9-12 插入节点 appendChild()

`appendChild()` 方法可在指定节点的**最后一个子节点列表之后**添加一个新的子节点。

语法：`appendChild(newnode)`

``` html
<!DOCTYPE HTML>
<html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
        <title>添加子节点</title>
    </head>
    <body>
        <ul id="test">
            <li>JavaScript</li>
            <li>HTML</li>
        </ul> 
        <script type="text/javascript">
            var otest = document.getElementById("test");
            var newnode = document.createElement("li");
            newnode.innerHTML = "PHP";
            otest.appendChild(newnode);
        </script> 
    </body>
</html>
```

## 9-13 插入节点 insertBefore()

`insertBefore()` 方法可在**已有的子节点前**插入一个新的子节点。

语法：`insertBefore(newnode,node)`

说明：<br>
newnode 参数为要插入的新节点；node 参数指定此节点前插入节点

``` html
<!DOCTYPE HTML>
<html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
        <title>添加子节点到指定子节点前</title>
    </head>
    <body>
        <ul id="test"><li>JavaScript</li><li>HTML</li></ul> 
        <script type="text/javascript">
            var otest = document.getElementById("test"); 
            var node = otest.childNodes[1];
            var newnode = document.createElement("li");
            newnode.innerHTML = "PHP";
            otest.insertBefore(newnode, node);
        </script>
    </body>
</html>
```

## 9-14 删除节点 removeChild()

`removeChild()` 方法可从子节点列表中删除某个节点。如删除成功，返回被删除的**节点**；如失败，则返回 NULL。

语法：`nodeObject.removeChild(node)`

如果还需要使用删除的子节点，可以把删除的子节点赋值给 x。这样这个子节点虽然不在 DOM 树中，但是还存在内存中，可通过 x 来操作它。之后可以通过给 x 赋 null 值来完全从内存中删除这个节点对象。

## 9-15 替换元素节点 replaceChild()

`replaceChild()` 方法可实现子节点(对象)的替换。返回被替换对象的引用。 

语法：`node.replaceChild (newnode,oldnew)`

说明: 
1. 当 oldnode 被替换时，所有与之相关的属性内容都将被移除 
2. newnode 必须先被建立

``` html
<!DOCTYPE HTML>
<html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
        <title>替换节点</title>
    </head>
    <body>
        <div><b id="oldnode">JavaScript</b></div>
        <a href="javascript:replaceMessage()">将加粗改为斜体</a>
        <script type="text/javascript">
            function replaceMessage(){
                var newnode=document.createElement("i");
                var oldnode=document.getElementById("oldnode");
                newnode.innerHTML = oldnode.innerHTML;
                oldnode.parentNode.replaceChild(newnode,oldnode);
            }    
        </script>
    </body>
</html>
```

## 9-16 创建元素节点 createElement

`createElement()` 方法可创建元素节点，并返回一个 Element 对象。

语法：`document.createElement(tagName)`

``` html
<!DOCTYPE HTML>
<html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
        <title>无标题文档</title>
    </head>
    <body>
        <script type="text/javascript">
            //创建链接
            function createa(url,text){
                var aline = document.createElement("a");
                aline.href=url;
                //aline.setAttribute("href",url);
                aline.innerHTML=text;
                document.body.appendChild(aline);
            }
            // 调用函数创建链接
            createa("http://www.imooc.com","慕课网");
        </script> 
    </body>
</html>
```
* 代码也可参考前面 '插入节点' 和 '替换节点' 中的代码

## 9-17 创建文本节点 createTextNode

`createTextNode()` 方法可创建新的文本节点，返回新创建的 text 节点。

语法：`document.createTextNode(data)`

如 '替换节点' 一节的代码中的：
``` js
newnode.innerHTML = oldnode.innerHTML;
```
也可以写成
``` js
var newtext=document.createTextNode(oldnode.innerHTML);
newnode.appendChild(newtext);
```
