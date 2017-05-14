title : 文件传输基础——Java IO流
date  : 2017/5/5

---

# 第1章	文件的编码

## 1-1 文件的编码

* 用项目默认编码或指定编码，将字符串转换成字节序列

``` java
getBytes();
getBytes(“gbk”);
```
* 文本文件是字节序列，可以放任意编码的字节序列

  对于指定的 Java 项目，只认识该项目的编码，在该项目上新建的文本文件也是符合这个编码；如果将这个文本文件直接拷贝到不同编码的 Java 项目中就会出现乱码，如果拷贝到系统上是不会出现乱码的；如果只复制粘贴文字内容，文本文件是可以自动转换的；如果在中文机器上直接创建文本文件，那么该文本文件只认识 ansi 编码



# 第2章	File类的使用

## 2-1 File类常用 API 介绍

*  `java.io.File` 类用于表示文件/目录

   `File` 类只用于表示文件/目录的信息（名称、大小等），不能用于文件内容个的访问  
  
*  `File` 类基本 API 操作

   构造函数、判断文件/文件夹是否存在、创建/删除文件夹、设置分隔符、判断是否是目录/文件、创建文件、打印目录/父目录、打印文件/目录名

## 2-2 遍历目录

### `File` 类的复杂使用

用 `list()` 方法和 `listFiles()` 方法，列出当前目录下的子目录和文件，或者列出当前目录下的所有内容包括子目录下的内容（递归）

# 第3章	RandomAccessFile类的使用

## 3-1 RandomAccessFile基本操作

 Java  提供的对文件内容的访问，既可以读文件也可以写文件；支持随机访问文件，可以访问文件的任意位置

* 文件模型

  在硬盘上的文件是byte byte byte存储的，是数据的集合

* 打开文件

    有两种模式“rw”（读写）、“r”（只读）

    在构造 `AccessFile` 的时候他要做的工作除了打开文件之外还要告诉他读写的方式（`RandomAccessFile raf = new RandomeAccessFile(file, “rw”)`）

    而且因为他是随机访问文件，所以他内部还含有一个文件指针，打开文件时指针在开头（`pointer = 0`），随着读写操作指针会往后挪

    随机读取文件文件有一个很大的好处是，（如迅雷）在下载文件的时候，特别是文件很大的时候，可以用多个程序去下载，每个程序下载一部分，最后再拼接成一个文件，这时候就要知道每部分是从哪里开始的，这时候就要用到 `RandomAccessFile`

* 写方法

    `write()` 方法，只能写一个字节，同时指针指向下一个位置准备再次写入

    也可以直接写一整个字节数组，或者用 `writeInt()` 直接写一个 `int`
    
* 读方法

  `seek(int x)`方法移动指针

  `read()`方法，只能读一个字节

    也可以把文件的内容一次性读到字节数组中

* 文件读写完成后一定要关闭，`close()`

# 第4章	字节流

IO 流是 java 作输入输出的基础，分为输入流和输出流，其中又分为字节流和字符流（ java 中读文件或者写文件的时候可以以字节为单位或者以字符为单位）

* 字节流对应输入输出有两个抽象的父类：`InputStream`（抽象了应用程序读取数据的方式）和 `OutputStream` （抽象了应用程序写出数据的方式）

* 达到文件结尾称为 EOF，=End ，或者读到 -1 也是读到结尾	

## 4-1 字节流之文件输入流 FileInputStream-1

## 4-2 字节流之文件输入流 FileInputStream-2

* 继承了 `InputStream` ，具体实现了在文件上读取数据

* 输入流的基本方法是读

    比如把键盘作为一个文件，然后我们往 txt 文件里写东西。这时键盘是输入，我们是从键盘这个文件读取了数据然后写到 txt 文件中。所以键盘是一个输入文件，是用来读的。

``` java
 int b = in.read();
 in.read(byte[] buf); 
 in.read(byte[] buf, int start, int size);
```
_*eg（文件内容的读取）_

## 4-3字节流之文件输出流 FileOutputStream

* 继承了 `OutputStream` ，具体实现了向文件中写出 byte 数据

* 输出流基本方法是写

``` java
out.write(int b); 
out.write(byte[] buf); 
out.write(byte[] buf, int start, int size);
```

_*eg（拷贝/复制文件）_

## 4-4 字节流之数据输入输出流

`DataInputStream / DateOutputStream` ，是对“流”功能的扩展，可以更加方便的读取 `int` 、 `long` 、字符等类型数据，也就是主要是操作类型数据的

* `DataOutputStream`

    `writeInt() / writeDouble() / writeUTF() `，这些都是以一种设计模式——装饰模式来实现的

* `DataInputStream` 同上理

## 4-5 字节缓冲流

`BufferedInputStream & BufferedOutputStream` ，这两个流类为 IO 提供了带缓冲区的操作，一般打开文件进行写入或读取操作时都会加上缓冲，这种流模式提高了 IO 的（输入输出）性能

* `FileOutputStream` 、 `DataOutputStream` 和`BufferedOutputStream` 的比较，输入流同理

* `System.currentTimeMills()`

_*eg（利用带缓冲的字节流进行文件拷贝）_

# 第5章	字符流

* 认识文本和文本文件

    java 的文本（`char`）是 16 位无符号整数，是字符的 unicode 编码（双字节编码）；文件是 byte byte byte ...的数据序列；

    文本文件是文本（`char`）序列按照某种编码方案序列化的 byte 储存结果。
* 字符流（ `Reader / Writer` ）

    一次处理一个字符，字符的底层仍然是基本的字节序列

    `InputStreamReader` 完成 byte 流解析为 char 流，按照编码解析

    `OutputStreamWriter` 提供 char 流到 byte 流，按照编码处理

    `FileReader / FileWriter`
    
## 5-1 字节字符转换流

## 5-2 字符流之文件读写流

同字节流理

## 5-3 字符流的过滤器

`BufferedReader / BufferedWriter / PrintWriter `，整行的读写操作 

# 第6章	对象的序列化和反序列化

* 对象序列化，就是将 Object 转换成 byte 序列，反之叫对象的反序列化

* 序列化流（ `ObjectOutputStream` ），字节过滤流，核心是 `writeObject()` ；反序列化流（ `ObjectInputStream` ），核心是 `readObj()`

* 序列化接口（ `Serializable` ）

    对象必须实现序列化接口，才能进行序列化，否则将出现异常

    这个接口没有任何方法，只是一个标准

## 6-1 序列化基本操作

## 6-2 transient 及 ArrayList 源码分析

*  `transient` 修饰的元素不会进行 jvm（虚拟机）默认的序列化

*  `defaultWriteObject()` ，把 jvm 能默认序列化的元素序列; `writeInt(age)` ， 自己进行元素的序列化

* `defaultReadObject()` ， `readInt()` 同上理

## 6-3 序列化中子父类构造函数问题

* 实现了序列化接口的类，其子类都可以实现序列化；

* 对子类对象进行序列化时会递归调用父类的构造函数；而对子类对象进行反序列化时，如果其父类没有实现序列化接口，那么其父类的构造函数会被调用