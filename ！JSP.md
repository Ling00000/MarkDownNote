title : Java Web 入门 —— JSP
date  : 2017/7/8
tags  : [Java Web, JSP]

---

Java Web 入门知识，主要包括 Java Web 开发环境搭建和工具使用、JSP 的基本语法、Java Web 开发思想。

<!--more-->

# 第1章 JAVA WEB 简介

## 1-1 什么是 WEB 应用程序

Web 应用程序是一种可以通过互联网访问的应用程序。用户只需要有浏览器并且联网就可以访问 Web 应用程序。

## 1-2 静态网页与动态网页

* 静态网页<br>
表现形式：网页中的内容是固定的，不会更新<br>
所需技术：HTML，CSS

* 动态网页<br>
表现形式：网页中的内容通过程序动态显示的，自动更新<br>
所需技术：HTML，CSS，数据库技术，Java/C#/Php，JavaScript，XML等。主流的动态网页脚本技术有 Jsp，Asp.net，Php

## 1-4 搭建 JAVA WEB 开发环境

搭建 Java Web 开发环境所需工具：JDK，Tomcat，MyEclipse

### Tomcat 服务器：

tomcat 服务器是常见的 Web 服务器，也是 JSP/Servlet 容器。tomcat 服务器的安装与配置过程如下：

1. 安装 tomcat<br>
下载相应版本的安装包后解压即可<br>
官方网站：[http://tomcat.apache.org/download-90.cgi](http://tomcat.apache.org/download-90.cgi)<br>
镜像网站：[http://mirror.bit.edu.cn/apache/tomcat/tomcat-9/v9.0.0.M21/bin/](http://mirror.bit.edu.cn/apache/tomcat/tomcat-9/v9.0.0.M21/bin/)
2. 配置环境变量<br>
添加环境变量 `CATALINA_HOME` ，变量值设置为 tomcat 所在目录
3. 测试首页<br>
在 tomcat 的 bin 目录下有一个 startup.dat 命令文件，用来启动服务器，点击后会弹出一个窗口，表示服务器已经启动，关闭之后服务器也会关闭。<br>
启动 tomcat 服务器之后，打开浏览器，输入网址 http://localhost:8080 ，回车后可以看到 Apache Tomcat 测试首页，说明 tomcat 安装完毕，一切正常

## 1-5 Tomcat 目录结构
 
/bin：存放各种平台下用于启动和停止 tomcat 的命令文件<br>
/conf：存放 tomcat 服务器的各种配置文件<br>
/lib：存放 tomcat 服务器所需的各种 jar 文件<br>
/logs：存放 tomcat 的日志文件<br>
/temp：tomcat 运行时用于存放临时文件<br>
/webapps：当发布 Web 应用时，默认会将 Web 应用的文件发布到此目录中<br>
/work：tomcat 把由 JSP 生成的 Servlet 放于此目录下<br>

## 1-6 手工编写第一个 Java Web 程序

1. 在 webapps 下创建项目目录

2. 在项目目录下新建一个 index.jsp，编写一个简单的 JSP 页面

3. 在项目目录下手动创建 WEB-INF 目录

4. 在手动创建的 WEB-INF 目录中新建一个 web.xml 文件，打开 webapps 下的 examples 实例参考目录的 WEB-INF 文件夹下的 web.xml，将其中的声明和 `<web-app>` 根标签拷贝过来

5. 在手动创建的 WEB-INF 目录下新建一个 classes 文件夹和一个 lib 文件夹，分别用于保存编译生成的字节码文件和需要用到的 jar 包

6. 测试运行，启动服务器，进入 localhost:8080 ，输入项目地址，打开 index.jsp，指定字符集调整乱码，就可以看到刚刚编写的 JSP 页面了

## 1-7 WEB-INF 目录详解

1. WEB-INF ，Java 的 WEB 应用的安全目录，所谓安全就是客户端无法访问，只有服务端可以访问的目录
2. web.xml，项目部署文件
3. classes 文件夹，用以放置 *.class 文件
4. lib 文件夹，用于存放需要的 jar 包

## 1-8 MyEclipse 开发 Java Web 程序

### MyEclipse ：
在 eclipse 基础上加上自己的插件开发而成的功能强大的企业级集成开发环境，主要用于 Java、Java EE 以及移动应用的开发。MyEclipse 的功能非常强大，支持也十分广泛，尤其是对各种开源产品的支持相当不错。

安装包下载：[http://www.myeclipsecn.com/bbs/?/question/246](http://www.myeclipsecn.com/bbs/?/question/246)

安装完成 MyEclipse，进行系统配置：

1. 配置 JRE ：<br>
 Windows -> Preference -> Java -> Installed JREs -> Add相应的JDK
2. 将 MyEclipse 集成 tomcat 服务器<br>
 Windows -> Preference -> Myeclipse -> Severs -> ServerRuntimeEnvironments -> Add相应的tomcat

部署项目到 tomcat 服务器：
工具栏ManageDeployment -> module -> 要进行部署的项目 -> Add相应的tomcat 

## 1-9 理解 Web 项目虚拟路径

我们之前在访问项目中的 JSP 页面是在地址栏填入的地址，可以理解为是项目的虚拟路径，虚拟路径默认跟项目的名字相同。

修改项目的虚拟路径：<br>
选择要操作的项目 -> Properties -> MyEclipse -> ProjectFacets -> Web -> 修改WebContextRoot -> 重新部署到服务器并重启

## 1-11 修改 Tomcat 服务器默认端口号

tomcat 默认占用的端口号是 8080，但在实际使用中有可能出现不同服务器端口号出现冲突的情况，这时候就要修改 tomcat 服务器的默认端口号。 

修改 tomcat 服务器默认端口号：<br>
tomcat根目录 -> conf -> server.xml -> 修改Connector标签的port属性

# 第2章 JSP 基础语法

## 2-1 JSP 简介

JSP 全名为 Java Sever Pages，其根本是一个简化的 Servlet 设计，实现了在 Java 当中使用 HTML 标签。JSP 是一种动态网页技术标准，也是 JAVAEE 的标准。JSP 与 Servlet 一样，是在服务器端执行的。

## 2-2 常见动态网站开发技术对比

JSP ：Java 平台，安全性高，适合开发大型的、企业级的 Web 应用程序

Asp.net ：.net 平台，简单易学，但是安全性及跨平台性差

PHP ：简单，高效，成本低，开发周期短，特别适合中小型企业的 Web 应用开发

## 2-3 JSP 页面元素简介及 page 指令

JSP 页面组成部分：指令，表达式，小脚本，声明，注释，静态内容

### JSP 指令：

1. `page` 指令：通常位于 jsp 页面的顶端，同一个页面可以有多个 page 指令

2. `include` 指令：将一个外部文件嵌入到当前 jsp 文件中，同时解析这个页面中的 jsp 语句

3. `taglib` 指令：使用标签库定义新的自定义标签，在 jsp 页面中启用定制行为

#### page 指令语法：

`<%@ page 属性1="属性值" 属性2="属性值1,属性值2" ... 属性n="属性值n"%>`

`page` 常用属性：

1. `language` ：指定 jsp 页面使用的脚本语言，默认为 java

2. `import` ：引用脚本语言中使用到的类库

3. `contentType` ：指定 jsp 页面所采用的字符编码以及文件类型。默认文件类型是 text/html ，表明是一个网页文本，默认的字符集是纯英文字符集 ISO-8859-1<br>
*注意：`pageEncoding` 是 jsp 文件本身的编码，而 `contentType` 中的 `charset` 是指服务器发给客户端是的内容编码。 `contentType` 更常用。

## 2-5 JSP 注释

1. HTML 注释：`<!--html注释-->`，客户端可见

2. JSP 注释：`<%--html注释--%>`，客户端不可见

3. JSP 脚本注释：`//单行注释`、`/*多行注释*/`，客户端不可见

## 2-7 JSP 脚本

在 jsp 页面中执行的 java 代码

语法：`<% java 代码 %>`

## 2-8 JSP 声明

在 jsp 页面中定义变量或者方法

语法：`<%! java 代码 %>`

## 2-9 JSP 表达式

在 jsp 页面中执行的表达式

语法：`<% =表达式 %>`

注意：表达式不以分号结束

## 2-10 JSP 页面生命周期

例如：用户使用客户端浏览器向服务器发送请求：<br>
1. 用户发出请求，访问 index.jsp
2. 判断是否是第一次请求，如果是，则执行 3 ，如果否，则跳过 3
3. tomcat JSP 引擎把该 jsp 文件转换成为一个 servlet，servlet 这个 java 类通过编译生成字节码文件，并执行其中的 `jspInit()` 方法进行初始化。这个初始化方法只在编译生成字节码文件的时候才执行，也就是在整个生命周期中只执行一次
4. 访问生成的字节码文件，解析执行其中的 `jspService()` 方法。其中 `jspServlet()` 方法就是用来处理用户的请求的。

### 关于 `jspServlet()` 方法

`jspServlet()` 方法被调用来处理客户端的请求。对每一个请求，jsp 引擎创建一个新的线程来处理该请求。如果有多个客户端同时请求该 jsp 文件，则 jsp 引擎会创建多个线程。每个客户端请求对应一个线程。以多线程方式执行可以大大降低对系统的资源需求，提高系统的并发量及响应时间。但也要注意多线程的编程带来的同步问题，由于该 servlet 始终驻于内存，所以响应是非常快的。

## 2-11 分别使用表达式和脚本实现打印九九乘法表
1. 使用表达式实现打印九九乘法表
``` jsp
<body>
<%!
//返回九九乘法表对应的 HTML 代码，通过表达式来调用，在页面上显示
    String printMultiTable1(){
        String s = "";
        for(int i=1;i<=9;i++)  			{
            for(int j=1;j<=i;j++)  				{
                s+=i+"*"+j+"="+(i*j)+"&nbsp;&nbsp;&nbsp;&nbsp";
            }
            s+="<br>";
        }
        return s;
    }
%>
<h1>九九乘法表</h1>
<hr>
<%=printMultiTable1() %>
</body>
```

2. 使用脚本实现打印九九乘法表
``` jsp
<body>
<%!
//jsp 内置  out 对象，使用脚本方式调用，打印就九九乘法表
    void printMultiTable2(JspWriter out)throws Exception    {
        for(int i=1;i<=9;i++){
            for(int j=1;j<=i;j++){
                out.println(i+"*"+j+"="+(i*j)+"&nbsp;&nbsp;&nbsp;&nbsp");
            }
            out.println("<br>");
        }	
    }
%>
<h1>九九乘法表</h1>
<hr>
<% printMultiTable2(out);%>
</body>
```

# 第3章 JSP 内置对象（上） 
## 3-1 JSP 内置对象简介

jsp 内置对象是 web 容器创建的一组对象，不使用 `new` 关键字就可以直接使用的内置对象。

### jsp 九大内置对象：
1. `out`
2. `request`
3. `response`
4. `session`
5. `application`
6. `Page` , `pageContext`, `exception` , `config` 

## 3-3 web 程序的请求与响应模式

web 程序是基于请求响应模式的——用户发送请求（request），服务器给用户响应（response）。

以登录程序为例：

1. 在登录窗口输入用户名和密码,然后点击登录按钮,就相当于客户端向服务器发送了请求,在请求对象中封装了用户名和密码
2. 请求发送到服务器后，服务器接收到用户的请求,判断用户名和密码正确之后，就给客户端发送响应页面

可以看出，web 应用程序是基于请求和响应的模式。

## 3-4 out对象 
### 缓冲区（Buffer）
所谓缓冲区就是内存的一块用来保存临时数据的区域。

### out 对象
`out` 对象是 `JspWriter` 类的实例，是向客户端输出内容常用的对象。

常用方法：
1. `void println()`：向客户端打印字符串
2. `void clear()`：清除缓冲区的内容，如果在 `flush()` 之后调用会抛出异常
3. `void clearBuffer()`：清除缓冲区的内容，如果在 `flush()` 之后调用不会抛出异常
4. `void flush()`：将缓冲区内容输出到客户端
5. `int getBufferSize()`：返回缓冲区字节数的大小，如不设缓冲区则为0
6. `int getRemaining()`：返回缓冲区还剩余多少可用
7. `boolean isAutoFlush()`：返回缓冲区满时，是自动清空还是抛出异常
8. `void close()`：关闭输出流

## 3-6 get 与 post 提交方式的区别

表单的标签中有三种常用的属性，其中有一个 `method` 属性,表示表单的提交方式。

表单的两种提交方式：

1. get ：以明文的方式通过 URL 提交数据，数据在 URL 中可以看到。提交的数据最多不超过 2KB 。安全性较低但效率比 post 方式高。适合提交数据量不大，安全性不高的数据。比如：搜索、查询等功能。
2. post ：将用户提交的信息封装在 HTML HEADER 内。适合提交数据量大，安全性高的用户信息。比如：注册、修改、上传等功能。

``` html
<body>
<h1>用户登录</h1>
<hr>
<form action="/ImoocLearning/doLogin.jsp" name="LoginForm" method="get">
    <table>
        <tr>
            <td>用户名：</td>
            <td><input type="text" name="username"/></td>
        </tr>
        <tr>
            <td>密码：</td>
            <td><input type="password" name="password"/></td>
        </tr>
        <tr>
            <td colspan="2"><input type="submit" value="登录"></td>
        </tr>
    </table>
</form>
</body>
```

## 3-7 request对象（上）  

客户端的请求信息被封装到 `request` 对象中，通过它才能了解到客户的需求，然后做出相应。它是 `HttpServletRequest` 类的实例。`request` 对象具有请求域，即完成客户端的请求之前，该对象一直有效。

常用方法：
1. `String getParameter(String name)`：返回 name 指定参数的参数值
2. `String[] getParameterValues(String name)`：返回包含参数 name 的所有值的数组
3. `void setAttribute(String,Object)`：存储此请求中的属性
4. `object getAttribute(String name)`：返回指定属性的属性值
5. `String getContentType()`：得到请求体的 MIME 类型
6. `String getProtocol()`：返回请求用的协议类型及版本号
7. `String getSeverName()`：返回接受请求的服务器主机名
8. `int getServerPort()`：返回服务器接受此请求所用的端口号
9. `String getCharacterEncoding()`：返回字符编码方式
10. `void setCharacterEcoding()`：设置请求的字符编码方式
11. `int getContentLength()`：返回请求体的长度（以字节数）
12. `String getRemoteAddr()`：返回发送此请求的客户端 IP 地址
13. `String getRealPath(String path)`：返回一虚拟路径的真实路径
14. `String request.getContextPath()`：返回上下文路径

``` jsp
<body>
<h1>request内置对象</h1>
<%
    request.setCharacterEncoding("utf-8");
    //只能解决中文乱码问题
    //想要解决 URL 传递中文出现的乱码问题需要配置tomcat服务器：
    //1.修改配置文档 sever.xml
    //2.为 Connector 标签添加属性：URLEncoding="utf-8"
    //3.保存文档重启 tomcat 服务器
%>
用户名：<%=request.getParameter("username") %><br>
爱好：<%
    if(request.getParameterValues("favorite")!=null){
        String[] favorites =request.getParameterValues("favorite");
        for(int i=0;i<favorites.length;i++){
            out.println(favorites[i]+"&nbsp;&nbsp");
        }
    }
    %>
</body>
```

## 3-8 request对象（下）

## 3-10 response对象 

`response` 对象包含了响应客户请求的有关信息，但在 jsp 中很少直接用到它。它是 HttpServletResponse 类的实例。 response 对象具有页面作用域，即访问一个页面是，该页面内的 response 对象只能对这次访问有效，其它页面的 response 对象对当前页面无效。

常用方法：
1. `String getCharacterEncoding()`：返回响应用的是何种字符编码
2. `void setContentType(String type)`：设置响应的 MIME 类型
3. `PrintWriter getWriter()`：返回可以向客户端输出字符的一个对象（PrinterWriter 打印时总是提前于内置 out 对象,可以用 `out.flush()` 方法将刷新 out 缓冲区来解决）
4. `sendRedirect(java.lang.String location)`：重新定向客户端的请求

## 3-11 请求重定向与请求转发的区别 

请求重定向：客户端行为， `response.sendRedirect()`；从本质上讲等同于两次请求，前一次的请求对象不会保存，地址栏的 URL 地址会改变。

请求转发：服务器行为，`request.getRequestDispatcher().forward(req.resp)`；是一次请求，转发后请求对象会保存，地址栏的 URL 地址不会改变。

# 第4章 JSP内置对象（下）  
## 4-1 什么是session 

`session` 表示客户端与服务器的一次会话。

Web 中的 `session` 指的是用户在浏览某个网站时，从进入网站到浏览器关闭所经过的这段时间，也就是用户浏览这个网站所花费的时间。`session` 实际上是一个特定的时间概念。

`session` 保存在服务器的内存中，并且不同用户对应有不同 `session`

## 4-2 session对象 

`session` 对象在第一个 jsp 页面被装载时自动创建，完成会话期管理。<br>
从一个客户打开浏览器并连接到服务器开始，到客户关闭浏览器离开这个服务器结束，被称为一个会话。<br>
当一个客户访问一个服务器时，可能会在服务器的几个页面之间切换，服务器应当通过某种办法知道这是一个客户，就需要 `session` 对象。<br>
`session` 对象是 `HttpSession` 类的实例。

常用方法：
1. `long getCreationTime()`：返回 session 创建时间
2. `public String getId()`：返回 session 创建时 jsp 引擎为它设的唯一 ID 号
3. `public Object setAttribute(String name, Object value)`：使用指定名称将对象绑定到此会话
4. `public Object getAttribute(String name)`：返回与此会话中的指定名称绑定在一起的对象，如果没有对象绑定在该名称下，则返回 null
5. `String[] getValueNames()`：返回一个包含此 session 中所有可用属性的数组
6. `int getMaxInactiveInterval()`：返回两次请求间隔多长时间（秒）此 session 被取消。

SessionP1.jsp
``` jsp
<body>
<h1>session 内置对象</h1>
<%
	SimpleDateFormat sdf = new SimpleDateFormat("yyyy年MM月dd日 HH:mm:ss");
	Date d = new Date(session.getCreationTime());
	session.setAttribute("username", "admin");
	session.setAttribute("password", "pass");
	session.setAttribute("age", "18");
	
	//设置当前 session 最大生成期限（秒）
	session.setMaxInactiveInterval(10);
%>
<hr>
session创建时间：<%=sdf.format(d) %><br>
session的ID编号：<%=session.getId() %><br> 
从session中获取用户名：<%=session.getAttribute("username") %><br>

<a href="SessionP2.jsp" target="_blank">跳转到 SessionP2.jsp</a>
</body>
```

SessionP2.jsp
``` jsp
<body>
<h1>session 内置对象</h1>
<hr>
session的ID编号：<%=session.getId() %><br> 
从session中获取用户名：<%=session.getAttribute("username") %><br>
session 中保存的属性有：<%
  						String[] names=session.getValueNames();
  						for(int i=0; i<names.length; i++){
  							out.println(names[i]+"&nbsp;&nbsp");
  						}	
%><br>
</body>
```

## 4-4 session的生命周期 

### 创建：
当客户端第一次访问某个 jsp 或者 Servlet 的时候，服务器会为当前会话创建一个 SessionId ，每次客户端向服务器发送请求是，都会将此 SessionId 携带过去，服务端会对此 SessionId 进行校检,看是否是同一次会话。

### 活动：
1. 某次会话当中通过超链接打开的新页面属于同一次会话。
2. 只要当前会话页面没有全部关闭，重新打开新的浏览器窗口访问同一项目资源时属于同一次会话。除非本次会话的所有页面都关闭后再次重新访问某个 jsp 或者 Servlet ，将会创建新的会话。<br><br>
注意：原有会话还存在，只是这个旧的 SessionId 存在于服务端，却再也没有客户端会携带它然后后交予服务端校验。

### 销毁：
session 的销毁只有三种方式：
1. 调用了 `session.invalidate()` 方法
2. session 过期/超时<br>
tomcat 默认 session 超时时间为 30 分钟；<br>
设置超时时间有两种方式：
   1. `session.setMaxInactiveInterval()`；（秒）
   2. 配置 web.xml：（分钟）
   ``` xml
   <session-config>
     <session-timeout>
       10
     </session-timeout>
   </session-config>
   ``` 
3. 服务器重新启动

## 4-6 application对象 

`application` 对象实现了用户间数据的共享，可存放全局变量。 `application` 开始于服务器的启动，终止于服务器的关闭。在用户的前后连接或不同用户之间的连接中，可以对 `application` 对象的同一属性进行操作。在任何地方对 `application` 对象属性的操作，都将影响到其他用户对此的访问。`application` 对象是 `ServletContext` 类的实例。

常用方法如下：
1. `public void setAttribute(String name, Object value)`：使用指定名称将对象绑定到此会话。
2. `public Object getAttribute(String name)`：返回与此会话中的指定名称绑定在一起的对象，如果没有对象绑定在该名称下，则返回 null。
3. `Enumeration getAttributeNames()`：返回所有可用属性名的枚举
4. `String getServerInfo()`：返回 JSP(SERVLET) 引擎名及版本号

``` jsp
<body>
<h1>application 内置对象</h1>
<%
  	application.setAttribute("city", "北京");
  	application.setAttribute("postcode", "10000");
  	application.setAttribute("email", "lisi@126.com");
%>
所在城市是：<%=application.getAttribute("city") %><br>
application中的属性有：<%
  	Enumeration attributes = application.getAttributeNames();
  	while(attributes.hasMoreElements()){
  		out.println(attributes.nextElement()+"&nbsp;&nbsp");
  	}
%><br>
JSP(SERVLET)引擎名及版本号：<%=application.getServerInfo() %><br>
</body>
```

## 4-8 page对象 

`page` 对象就是指向当前 jsp 页面本身，有点像类中的 this 指针，它是 `java.lang.Object` 类的实例。

常用方法：
1. `class getClass()`：返回此 Object 的类
2. `int hashCode()`：返回此 Object 的 hash 码
3. `boolean equals(Object obj)`：判断此 Object 是否与指定的 Object 对象相等 
4. `void copy(Object obj)`：把此 Object 拷贝到指定的 Object 对象中
5. `Object clone()`：克隆此 Object 对象
6. `String toString()`：把此 Object 对象转换成 String 类的对象
7. `void notify()`：唤醒一个等待的线程
8. `void notifyAll()`：唤醒所有等待的线程
9. `void wait(int timeout)`：使一个线程处于等待直到 timeout 结束或被唤醒
10. `void wait()`：使一个线程处于等待直到被唤醒

## 4-9 pageContext对象和config对象 

### pageContext对象

`pageContex` 对象提供了对 jsp 页面内所有的对象及名字空间的访问，可以访问到本页所在的 session，也可以取本页面所在的 application 的某一属性值。`pageContext` 对象相当于页面中所有功能的集大成者。

常用方法：
1. `JspWriter getOut()`：返回当前客户端响应被使用的 JspWriter 流（out）
2. `HttpSession getSession()`：返回当前页中的 HttpSession 对象（session）
3. `Object getPage()`：返回当前页的 Object 对象（page）
4. `ServletRequest getRequest()`：返回当前页的 ServletRequest 对象（request）
5. `ServletResponse getResponse()`：返回当前页的 ServletResponse 对象（response）
6. `void setAttriute(String name, Object attribute)`：设置属性及属性值
7. `Object getAttribute(String name, int scope)`：在指定范围内取属性的值
8. `int getAttributeScope(String name)`：返回某属性的作用范围
9. `void forward(String relativeUrlPath)`：使当前页面重导到另一页面
10. `void include(String relativeUrlPath)`：在当前位置包含另一文件

### config对象

`config` 对象时在一个 Servlet 初始化时， jsp 引擎向它传递信息用的，此信息包括 Servlet 初始化时所要用到的参数（通过属性名和属性值构成）以及服务器的有关信息（通过传递一个 ServletContext 对象）

常用方法：
1. `ServletContext getServletContext()`：返回含有服务器相关信息的 ServletContext 对象
2. `String getInitParameter(String name)`：返回初始化参数的值
3. `Enumeration getInitParameterNames()`：返回 Servlet 初始化所需所有参数的枚举

## 4-10 exception对象 

`exception` 对象是一个异常对象，当一个页面在运行过程中发生了异常，就产生这个对象。如果一个 jsp 页面要应用此对象，就必须把 isErrorPage 设为 true，并且把产生该对象的出错页面的 errorPage 设置为该 jsp 页面。它实际上是 java.lang.Throwable 的对象。

常用方法：
1. `String getMessage()`：返回描述异常的消息
2. `String toString()`：返回关于异常的简短描述消息
3. `void printStackTrace()`：显示异常及其栈轨迹
4. `Throwable FillInStackTrace()`：重写异常的执行栈轨迹

## 4-11 阶段案例——实现用户登录

说明：不适用数据库，指定了唯一的合法用户，用户名是 admin ，密码是 admin ，登录成功使用服务器内部转发到 login_success.jsp 页面，并且提示登陆成功的用户名。如果登录失败则请求重定向到 login_failure.jsp 页面。

Login.jsp
``` html
<body>
<div id="container">
    <div id="box">
        <form action="A_doLogin.jsp" method="post">
        <p class="main">
            <label>用户名：</label>
            <input name="username" value=""/>
            <label>密码：</label>
            <input type="password" name="password" value=""/>
        </p>
        <p class="space">
            <input type="submit" value="登录" class="login" style="cursor: pointer;"/>
        </p>	
        </form>
    </div>
</div>
</body>
```

doLogin.jsp
``` jsp
<%
String path = request.getContextPath();
String basePath = request.getScheme()+"://"+request.getServerName()+":"+request.getServerPort()+path+"/";

String username="";
String password="";
request.setCharacterEncoding("utf-8");
username = request.getParameter("username");
password = request.getParameter("password");
if("admin".equals(username) && "admin".equals(password)){
	session.setAttribute("loginUser", username);
	request.getRequestDispatcher("A_login_success.jsp").forward(request, response);
}else{
	response.sendRedirect("A_login_failure.jsp");
}
%>
```

login_success.jsp
``` jsp
<body>
<div id="container">
    <div id="box">
        <%
            String loginUser = "";
            if(session.getAttribute("loginUser")!=null){
                loginUser = session.getAttribute("loginUser").toString();
            }
        %>
        <%=loginUser %>,登录成功！
    </div>
</div>
</body>
```

login_failure.jsp
``` jsp
<body>
<div id="container">
    <div id="box">
        登录失败！请检查用户名或者密码！<br>
        <a href="A_Login.jsp">返回登录</a>
    </div>
</div>
</body>
```

# 第5章 JavaBeans

## 5-2 JavaBean简介及设计原则

javabeans 就是符合某种特定的规范的 Java 类。使用 Javabeans 的好处是解决代码重复编写，减少代码冗余，功能区分明确，提高了代码的维护性。

所谓的特定规范也可以理解为 Javabean 的设计原则。

### Javabean 的设计原则：
1. 是公有类；
2. 包含无参的公有构造方法；
3. 属性是私有的；
4. 使用 `getter` 和 `setter` 方法对属性进行封装

eg：
``` java
//公有类
public class Users{

    //私有属性
    private String username;
    private String password;

    //无参的公有构造方法
    public Users(){
    }

    // getter，setter 方法
	public String getUsername() {
		return username;
	}
	public void setUsername(String username) {
		this.username = username;
	}
	public String getPassword() {
		return password;
	}
	public void setPassword(String password) {
		this.password = password;
	}
}
```

## 5-3 什么是JSP动作元素

JSP 动作元素（ action elements ），动作元素为请求处理阶段提供信息。动作元素简单来说就是一个标签，遵循 XML 元素的语法，有一个包含元素名的开始标签，可以有属性、可选的内容、与开始标签相匹配的结束标签。

### 五大类 JSP 动作元素：

第一类是与存取 JavaBean 有关的，包括：<br>
`<jsp:useBean> <jsp:setProperty> <jsp:getProperty>`

第二类是 JSP1.2 就开始有的基本元素，包括 6 个动作元素：<br>
`<jsp:include> <jsp:forward> <jsp:param> <jsp:plugin> <jsp:params> <jsp:fallback>`

第三类是 JSP2.0 新增加的元素，主要与 JSP Document 有关，包括 6 个元素：<br>
`<jsp:root> <jsp:declaration> <jsp:scriptlet> <jsp:expression> <jsp:text> <jsp:output>`

第四类是 JSP2.0 新增的动作元素，主要是用来动态生成 XML 元素标签的值，包括 3 个动作：<br>
`<jsp:attribute> <jsp:body> <jsp:element>`

第五类是 JSP2.0 新增的动作元素，主要是用在 Tag File 中，有 2 个元素：<br>
`<jsp:invoke> <jsp:dobody>`

## 5-4 使用普通方式创建JavaBean

在 jsp 页面中如何使用 Javabeans：<br>
1、像使用普通 java 类一样，创建使用 javabean 实例，如 5-2 中例

``` jsp
<body>
<%
    Users user = new Users();
    user.setUsername("adminN");
    user.setPassword("adminP");
%>
<h1>使用普通方式创建 javabean 的实例</h1>
<hr>
用户名：<%=user.getUsername() %><br>
密码：<%=user.getPassword() %><br>
</body>
```

## 5-5 useBean动作元素

在 jsp 页面中如何使用 Javabeans：<br>
2、在 jsp 页面中通常使用 jsp 动作标签使用 javabean,主要有：useBeans动作，setProperty动作，getProperty动作

### \<jsp:useBeans>

在 jsp 页面中实例化或者在指定范围内使用 javabean 。

语法：
```jsp
<jsp:useBean id="标示符" class="java类名" scope="作用范围"/>
```

``` jsp
<body>
<jsp:useBean id="myUsers" class="JBeanLearning.Users" scope="page"/>
<h1>使用 useBean 动作创建 javabean 的实例</h1>
<hr>
用户名：<%=myUsers.getUsername() %><br>
密码：<%=myUsers.getPassword() %><br>
</body>
```

## 5-6 setProperty

给已经实例化的 Javabean 对象的属性赋值，一共有四种形式。

语法：
```jsp
//跟表单关联
<jsp:setProperty name="JavaBean实例名" property="*" />
//跟表单关联
<jsp:setProperty name="JavaBean实例名" property="JavaBean属性名" />
//手工设置
<jsp:setProperty name="JavaBean实例名" property="JavaBean属性名" value="BeanValue" />
//跟 request 参数关联
<jsp:setProperty name="JavaBean实例名" property="propertyName" param="request对象中的参数名" />
```

## 5-7 getProperty

获取指定 Javabean 对象的属性值。

语法：
``` jsp
<jsp:getProperty name="JavaBean实例名" property="属性名" />
```

## 5-8 JavaBean四个作用域范围

使用 useBeans 的 scope 属性 可以用来指定 Javabean 的作用范围，主要有四种：
1. page：仅在当前页面有效
2. request；可以通过 `HttpRequest.getAttribute()` 方法取得 JavaBean 对象
3. session；可以通过 `HttpSession.getAttribute()` 方法取得 JavaBean 对象
4. application：可以通过 `application.getAttribute()` 方法取得 JavaBean 对象

## 5-10 Model1简介

在 Model1 模型出现前，整个 Web 应用的情况：几乎全部由 Jsp 页面组成，Jsp 页面接收处理客户端请求，对请求处理后作出响应。这样的弊端是：在界面层充斥着大量的业务逻辑代码和数据访问层的代码，Web 程序的可扩展性和可维护性非常差。

Javabean 的出现可以使 jsp 页面中使用 Javabean 封装的数据或者调用 Javabean 的业务逻辑代码，这样大大提升了程序的可维护性。

Model1 模型就是 jsp+javabean 的组合，将界面、业务逻辑和数据三层分离开来提高程序的可维护性，体现了分层设计的思想。

## 5-12 阶段项目——使用jsp+javabean完成用户登录功能

说明：使用 Model1 这种开发模式继续完善上一章——jsp内置对象的项目案例


``` java
/**
 * 用户类
 */
public class Users {
	private String username;//用户名
	private String password;//密码
	
	//保留此默认的构造方法
	public Users(){
	}

	public String getUsername() {
		return username;
	}
	public void setUsername(String username) {
		this.username = username;
	}
	public String getPassword() {
		return password;
	}
	public void setPassword(String password) {
		this.password = password;
	}
}
```

``` java
/**
 * 用户的业务逻辑类
 */
public class UsersDAO {
	//用户登录方法
	public boolean usersLogin(Users u){
		if("admin".equals(u.getUsername()) && "admin".equals(u.getPassword())){
			return true;
		}else{
			return false;
		}
	}
}
```

``` html
<!-- Login.jsp -->
<body>
<div id="container">
    <div id="box">
        <form action="doLogin.jsp" method="post">
        <p class="main">
            <label>用户名：</label>
            <input name="username" value=""/>
            <label>密码：</label>
            <input type="password" name="password" value=""/>
        </p>
        <p class="space">
            <input type="submit" value="登录" class="login" style="cursor: pointer;"/>
        </p>	
        </form>
    </div>
</div>
</body>
```

``` jsp
<%-- doLogin.jsp --%>
<%
	request.setCharacterEncoding("utf-8");
%>
<jsp:useBean id="Users" class="JBeanLearning.Users" scope="page"/>
<jsp:useBean id="userDAO" class="JBeanLearning.UsersDAO" scope="page"/>
<jsp:setProperty property="*" name="Users"/>
<%
	String path = request.getContextPath();
	String basePath = request.getScheme()+"://"+request.getServerName()+":"+request.getServerPort()+path+"/";
	
	if(userDAO.usersLogin(Users)){
		session.setAttribute("loginUser", Users.getUsername());
		request.getRequestDispatcher("A_login_success.jsp").forward(request, response);
	}else{
		response.sendRedirect("A_login_failure.jsp");
	}
%>
```


# 第6章 JSP状态管理

## 6-1 http协议的无状态性

无状态是指，当浏览器发送请求给服务器的时候，服务器响应客户端请求；但是当同一个浏览器再次发送请求给服务器的时候，服务器并不知道它就是刚才的那个浏览器。

简单地说，就是服务器不会去记得你，所以就是无状态协议。

## 6-2 Cookie概述

保存用户状态的两大机制：会话对象Session和客户端技术Cookie

### Cookie ：
是 Web 服务器保存在客户端的一系列文本信息。

典型应用一：判断注册用户是否已经登录网站<br>
典型应用二：“购物车”的处理

### Cookie的作用：
1. 对特定对象的追踪
2. 保存用户网页浏览记录与习惯
3. 简化登录

### 安全风险：
容易泄露用户信息

## 6-3 JSP页面中创建与使用Cookie

创建Cookie对象：<br>
`Cookie newCookie = new Cookie(String key, Object value)`

写入Cookie对象：<br>
`response.addCookie(newCookie)`

读取Cookie对象：<br>
`Cookie[] cookies = request.getCookies()`

常用方法：
1. `void setMaxAge(int expiry)`：设置 cookie 的有效期（秒）
2. `void setValue(String value)`：在 cookie 创建后，对 cookie 进行赋值
3. `String getName()`：获取 cookie 的名称
4. `String getValue()`：获取 cookie 的值
5. `int getMaxAge()`：获取 cookie 的有效时间（秒）


## 6-4 案例：Cookie在登录中的应用

实现记忆用户名和密码功能

LoginForm.jsp
``` jsp
<body>
    <h1>用户登录</h1>
    <hr>
    <%
  		String username="";
  		String password="";
  		Cookie[] cookies = request.getCookies();
		if(cookies!=null && cookies.length>0){
			for(Cookie c:cookies){
				if(c.getName().equals("username")){
					username=c.getValue();
				}
				if(c.getName().equals("password")){
					password=c.getValue();
				}
			}
		}
  	%>
  	<form name="loginForm" action="doLogin.jsp" method="post">
     	<table>
    		<tr>
    			<td>用户名：</td>
    			<td><input type="text" name="username" value="<%=username%>"/></td>
    		</tr>
    		<tr>
    			<td>密码：</td>
    			<td><input type="password" name="password" value="<%=password%>"/></td>
    		</tr>
    		 <tr>
    		 	<td colspan="2"><input type="checkbox" name="isUseCookie" checked="checked"/>十天内记住我的登录状态</td>
    		 </tr>
    		 <tr>
    		 	<td colspan="2"><input type="submit" value="登录"></td>
    		 </tr>
    	</table>
    </form>
</body>
```

doLogin.jsp
``` jsp
<body>
  	<h1>登录成功</h1>
  	<hr>
  	<br>
  	<br>
  	<br>
  	<%
  		//首先判断用户是否选择了记住登录状态
  		String[] isUseCookies = request.getParameterValues("isUseCookie");
  		if(isUseCookies!=null && isUseCookies.length>0){
  			//把用户名和密码保存在cookie对象里面
  			String username = request.getParameter("username");
  			String password = request.getParameter("password");
  			Cookie usernameCookie = new Cookie("username",username);
  			Cookie passwordCookie = new Cookie("password",password);
  			usernameCookie.setMaxAge(864000);
  			passwordCookie.setMaxAge(864000);//设置最大生存期限为10天
  			response.addCookie(usernameCookie);
  			response.addCookie(passwordCookie);
  		}else{
  			Cookie[] cookies = request.getCookies();
  			if(cookies!=null && cookies.length>0){
  				for(Cookie c:cookies){
  					if(c.getName().equals("username") || c.getName().equals("password")){
  						c.setMaxAge(0);//设置Cookie失效
  						response.addCookie(c);//重新保存
  					}
  				}
  			}
  		}
  	%>
</body>
```

## 6-5 Session与Cookie的对比

### session
1. 在**服务器**端保存用户信息
2. session 中保存的是 **Object** 类型
3. 随会话的结束而将其存储的数据**销毁**
4. 保存**重要**的信息

### cookie
1. 在**客户端**保存用户信息
2. cookie 保存的是 **String** 类型
3. cookie 可以**长期**保存在客户端
4. 保存**不重要**的用户信息


# 第7章 JSP指令与动作元素

## 7-1 include指令

语法：`<%@ include file="URL"%>`

## 7-2 include动作

语法：`<jsp:include page="UrL" flush="true|false"/>`

说明：`page`属性表示要包含的页面，`flush`属性表示被包含的页面是否从缓冲区读取

## 7-3 include指令与include动作的区别

### include指令
1. **页面转换**期间发生作用
2. 包含的内容是**文件的实际内容**
3. 主页面和包含页面转换为**一个**Servlet
4. 资源在**编译时**被解析，因此编译时间较慢，执行时间稍快

### include动作
1. 在**请求**期间发生作用
2. 内容是**页面的输出**
3. 主页面和包含页面转换为**独立**的Servlet
4. 资源在**执行时**被解析，因此执行时间较慢，编译时间稍快

## 7-4 forward动作

语法：`<jsp:forward page="URL"/>`

说明：等同于 `request.getRequestDispatcher("/url").forward(request, response)` ，实现请求转发

## 7-5 param动作

语法：`<jsp:param name="参数名" value="参数值">`

说明：常常与 `<jsp:forward>` 一起使用，作为其子标签，可以添加新的参数或者修改原有的参数

# 第8章 熟悉cookie实际应用——项目案例：商品浏览记录的实现

## 1、总体介绍
采用 Model1（Jsp+Javabean）实现；
开发步骤：
1. 实现 DBHelper 类：操作数据库，显示所用的商品信息（创建数据库连接对象）
2. 创建实体类：跟数据库中的商品表是一一对应的




