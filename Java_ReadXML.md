title : 结合 Java 程序的 XML（一）
date  : 2017/5/14

---

# 文件读取

## 第1章 与 XML 的初次邂逅

初识 xml 

表现：以“.xml”为扩展名的文件

存储结构：树形结构

例如：
```
<?xml version="1.0" encoding="UTF-8"?>
<bookstore>
    <book id="1">
        <name>BOOKone</name>
        <author>Tom</author>
    </book>
    <book id="2">
        <name>BOOKtwo</name>
        <year>2017</year>
    </book>
</bookstore>
```
* 值得一提的是，在写 xml 正文之前要写一个声明，内容是主要是版本和编码

主要作用：要实现不同应用程序间和不同平台间的通信，以及不同平台间的数据共享，可以用 xml 文件将他们联系起来

## 第2章 应用 DOM 方式解析 XML

在 Java 程序中读取 xml 文件内容的过程也称为**解析 xml 文件**；解析后可以获取 xml 中的节点名、节点值、属性名、属性值； 主要有四种解析方式，其中 DOM 解析和 SAX 解析是 Java 提供的 xml 的官方解析方式，而 DOM4J 解析和 JDOM 解析不是官方的需要另外下载 jar 包。

### 2-1 如何进行 XML 文件解析前的准备工作

``` java
// 创建一个 DocumentBuilderFactory 的对象
DocumentBuilderFactory dbf = DocumentBuilderFactory.newInstance();
//创建 DocumentBuilder 对象
DocumentBuilder db = dbf.newDocumentBuilder();
//通过 DocumentBuilder 对象的 parser 方法加载文件到当前项目下
Document document = db.parse("book.xml");

//获取所有 book 节点的集合
NodeList bookList = document.getElementsByTagName("book");
//通过 NodeList 的 getLength() 方法法额可以获取 bookList 的长度
System.out.println("一共有"+bookList.getLength()+"本书");
//遍历每一个 book 节点
for(int i=0; i < bookList.getLength(); i++){
	//通过 item(i) 方法获取一个 book 节点， NodeList 的索引值从 0 开始
	Node book = bookList.item(i);
	//遍历 book 节点的所有属性集合
	NamedNodeMap attrs = book.getAttributes();
	System.out.println("第" + (i+1) + "本书共有" + attrs.getLength() + "个属性");
	System.out.println("****下面开始遍历第" + (i+1) + "本书的内容****");
```
* 注意捕获异常

### 2-2 使用 DOM 解析 XML 文件的属性名和属性值

``` java				
	//遍历 book 的属性
	for(int j=0; j<attrs.getLength(); j++){
		//通过 item(index) 方法获取 book 节点的某一个属性
		System.out.println("####遍历读取第" + (i+1) + "本书的属性");
		Node attr = attrs.item(j);
		//获取属性名
		System.out.print("属性名：" + attr.getNodeName());
		//获取属性值
		System.out.println("--属性值" + attr.getNodeValue());
	}
					
	//若已经知道 book 节点有且只有 1 个 id 属性
	System.out.println("####读取第" + (i+1) + "本书的 id 属性");
	//将 book 节点进行强制类型转换，转换成 Element 类型
	Element book1 = (Element) bookList.item(i);
	//通过 getAttribute("id") 方法获取属性值
	String attrValue = book1.getAttribute("id");
	System.out.println("id 属性的属性值为"+attrValue);		
```

### 2-3 使用 DOM 解析 XML 文件的节点名和节点值

``` java
	//解析 book 节点的子节点
	NodeList childNodes = book.getChildNodes();
	//遍历 childNodes 获取每个节点的节点名和节点值
	System.out.println("第" + (i+1) + "本书" +childNodes.getLength()+ "个子节点");
	for(int k=0; k<childNodes.getLength(); k++){
		//区分出 Text 类型的 node 和 Element 类型的 node
		if(childNodes.item(k).getNodeType() == Node.ELEMENT_NODE){
			//获取了 Element 类型节点的节点名
			System.out.print("第"+(k+1)+"个节点的节点名："+childNodes.item(k).getNodeName());
			System.out.println("--节点值是："+childNodes.item(k).getFirstChild().getNodeValue());
		}
	}
				
	System.out.println("****结束遍历第" + (i+1) + "本书的内容****");
}
```

* Java 程序在解析 xml 文档时会把**开始**和**结束**标签中的所有内容都看做是子节点，文字类型的部分（如空白和换行）会看成是 Text 类型的节点，带标签的部分就会看成是 Element 类型的节点。

* Element 类型会把 `<name>BOOKone</name>` 中间的 BOOKone 看成是 name 的子节点，所以想要获取 “ BOOKone ” 要先获取 name 的子节点在获取节点值，即 `.getFirstChild().getNodeValue()` 

* 比较区分 `getTextContent()` 和 `getFirstChild().getNodeValue()`

## 第3章 应用 SAX 方式解析 XML

**DOM 解析和 SAX 解析的比较:**

DOM 解释是将 xml 文件整个加载到内存中然后逐个解析

SAX 解析是通过一个自己创建的 Handle 处理类由外向里按顺序逐个分析每个节点然后解析出来

### 3-1 使用 SAX 解析 XML 文件的开始和结束

``` java
//获取一个 SAXParserFactory 实例
SAXParserFactory factory = SAXParserFactory.newInstance();
//通过 factory 获取 SAXParser 实例
SAXParser parser = factory.newSAXParser();
//创建一个类继承 DefaultHandler ，重写其中的一些方法进行业务处理，并创建这个类的实例
//创建 SAXParserHandler 对象
SAXParserHandler handler = new SAXParserHandler();
			parser.parse("book.xml", handler);
```
* 注意捕获异常

``` java
public class SAXParserHandler extends DefaultHandler {
	
	//用来标识解析开始
	@Override
	public void startDocument() throws SAXException {
		// TODO 自动生成的方法存根
		super.startDocument();
		System.out.println("SAX 解析开始");
	}

	//用来标识解析结束
	@Override
	public void endDocument() throws SAXException {
		// TODO 自动生成的方法存根
		super.endDocument();
		System.out.println("SAX 解析结束");
	}

	//用来遍历 xml 文件的开始标签
	@Override
	public void startElement(String uri, String localName, String qName, Attributes attributes) throws SAXException {
		// TODO 自动生成的方法存根
		super.startElement(uri, localName, qName, attributes);

	}
	
	//用来遍历 xml 文件的结束标签
	@Override
	public void endElement(String uri, String localName, String qName) throws SAXException {
		// TODO 自动生成的方法存根
		super.endElement(uri, localName, qName);
	}
	
}
```

### 3-2 使用 SAX 解析 XML 文件的节点属性

``` java
	//用来遍历 xml 文件的开始标签
	@Override
	public void startElement(String uri, String localName, String qName, Attributes attributes) throws SAXException {
		// TODO 自动生成的方法存根
		super.startElement(uri, localName, qName, attributes);
		if(qName.equals("book")){
			//开始解析 book 元素的属性
			System.out.println("***开始遍历***");
			//已知 book 元素下属性的名称，根据属性名称获取属性值
			String value = attributes.getValue("id");
			System.out.println("book的属性值是：" + value);
			
			//不知道 book 元素下属性的名称以及个数
			int num = attributes.getLength();
			for(int i=0; i<num; i++){
				System.out.print("book元素的第" + (i+1) + "个属性名是" + attributes.getQName(i));
				System.out.println("---属性值是："+ attributes.getValue(i));
			}
		}
```
### 3-3 使用 SAX 解析 XML 文件的节点名和节点间文本

``` java
		else if(!qName.equals("book") && !qName.equals("bookstore")){
			System.out.print("节点名是：" + qName +"--");
		}
	}
	
	//用来遍历 xml 文件的结束标签
	@Override
	public void endElement(String uri, String localName, String qName) throws SAXException {
		// TODO 自动生成的方法存根
		super.endElement(uri, localName, qName);
		//判断是否针对一个节点遍历结束
		if(qName.equals("book")){
			System.out.println("***遍历结束***");
		}
	}
		
	@Override
	public void characters(char[] ch, int start, int length) throws SAXException {
		// TODO 自动生成的方法存根
		super.characters(ch, start, length);
		String value = new String(ch, start, length);
		if(!value.trim().equals("")){
			System.out.println(value);	
		}
	}
```

### 3-4 使用 SAX 解析将 XML 内容和结构存入 JAVA 对象

``` java
public class Book {
	private String id;
	private String name;
	private String author;
	private String year;
	public String getId() {
		return id;
	}
	public void setId(String id) {
		this.id = id;
	}
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public String getAuthor() {
		return author;
	}
	public void setAuthor(String author) {
		this.author = author;
	}
	public String getYear() {
		return year;
	}
	public void setYear(String year) {
		this.year = year;
	}
}
```
``` java
String value = null;
Book book = null;
private ArrayList<Book> bookList = new ArrayList<Book>();
public ArrayList<Book> getBookList() {
	return bookList;
}

public void startElement(String uri, String localName, String qName, Attributes attributes) throws SAXException {
	// TODO 自动生成的方法存根
	super.startElement(uri, localName, qName, attributes);
	if(qName.equals("book")){
		//创建一个 Book 对象
		book = new Book();
		//开始解析 book 元素的属性
		System.out.println("***开始遍历***");
		//已知 book 元素下属性的名称，根据属性名称获取属性值
		String value = attributes.getValue("id");
		System.out.println("book的属性值是：" + value);
		
		//不知道 book 元素下属性的名称以及个数
		int num = attributes.getLength();
		for(int i=0; i<num; i++){
			System.out.print("book元素的第" + (i+1) + "个属性名是" + attributes.getQName(i));
			System.out.println("---属性值是："+ attributes.getValue(i));
			if(attributes.getQName(i).equals("id")){
				book.setId(attributes.getValue(i));
			}
		}
	}
	else if(!qName.equals("book") && !qName.equals("bookstore")){
		System.out.print("节点名是：" + qName +"--");
	}
}
	
//用来遍历 xml 文件的结束标签
@Override
public void endElement(String uri, String localName, String qName) throws AXException {
	// TODO 自动生成的方法存根
	super.endElement(uri, localName, qName);
	//判断是否针对一个节点遍历结束
	if(qName.equals("book")){
		bookList.add(book);
		book = null;
		System.out.println("***遍历结束***");
	}
	else if(qName.equals("name")){
		book.setName(value);
	}
	else if(qName.equals("author")){
		book.setAuthor(value);
	}
	else if(qName.equals("year")){
		book.setYear(value);
	}
}
	
@Override
public void characters(char[] ch, int start, int length) throws SAXException {
	// TODO 自动生成的方法存根
	super.characters(ch, start, length);
		value = new String(ch, start, length);
	if(!value.trim().equals("")){
		System.out.println(value);	
	}
}
```
``` java
System.out.println("---共有" + handler.getBookList().size() + "本书---");
for(Book book : handler.getBookList()){
	System.out.println(book.getId());
	System.out.println(book.getName());
	System.out.println(book.getAuthor());
	System.out.println(book.getYear());
	System.out.println("---finish---");
}
```

## 第4章 应用 DOM4J 及 JDOM 方式解析 XML

### 4-1  JDOM 开始解析前的准备工作
在当前项目下选择 构建路径 -> 添加外部归档 ，然后选择下载好的 JDOM 的 jar 包添加进去，我使用的是 jdom2-2.0.5 版本；

在当前项目下新建一个 resource 文件夹，将要解析的 xml 文件放进去；

``` java
//准备工作
//1.创建一个 SAXBuilder 对象
SAXBuilder saxBuilder = new SAXBuilder();
InputStream in;
//2.创建一个输入流，将 xml 文件加载到输入流中
in = new FileInputStream("src/res/books.xml");
//3.通过 saxBuilder 的 build 方法，将输入流加载到 saxBuilder 中
Document document = saxBuilder.build(in);
//4.通过 document 对象获取 xml 文件的根节点
Element rootElement = document.getRootElement();
//5.获取根节点下的子节点的 List 集合
List<Element> bookList = rootElement.getChildren();
```
* 注意捕获异常

### 4-2 应用 JDOM 解析节点属性
```java
//继续进行解析
for(Element book: bookList){
	System.out.println("---开始解析第"+ (bookList.indexOf(book)+1) +"本书---");
	//解析 book 的属性集合
	List<Attribute> attrList = book.getAttributes();
	//知道节点下属性名称时，获取属性值：book.getAttributeValue("id");
	//遍历 attrList（不清楚 book 节点下属性的名字及数量时）
	for(Attribute attr: attrList){
		//获取属性名
		String attrName = attr.getName();
		//获取属性值
		String attrValue = attr.getValue();
		System.out.println("属性名："+ attrName +"---属性值："+ attrValue);
	}
```

### 4-3 应用 JDOM 解析子节点的名和值
```java
//对 book 节点的子节点的节点名以及节点值的遍历
List<Element> bookChilds = book.getChildren();
for(Element child: bookChilds){
	System.out.println("节点名："+ child.getName() +"---节点值："+ child.getValue());
}
System.out.println("---结束解析第"+ (bookList.indexOf(book)+1) +"本书---");
```

### 4-4  JDOM 解析是乱码的处理

1. 首先考虑修改 xml 文件的 `encoding` 属性，将它改为比较合适的字符集；

2. 当修改 `encoding` 还是不能达到解决效果时，对代码进行修改，将 `InputStream` 流进一步包装成 `InputStreamReader` ，并且在创建 `InputStreamReader` 对象时就指定好字符集：
``` java
in = new FileInputStream("src/res/books.xml");
InputStreamReader isr = new InputStreamReader(in, "UTF-8");
Document document = saxBuilder.build(isr);
```

### 4-5 在 JDOM 中存储 Book 对象
同样先创建一个 Book 类
``` java
private static ArrayList<Book> booksList = new ArrayList<Book>();
	
	public static void main(String[] args) {
		//进行对 books.xml 文件的 JDOM 解析
		//准备工作
		//1.创建一个 SAXBuilder 对象
		SAXBuilder saxBuilder = new SAXBuilder();
		InputStream in;
		try {
			//2.创建一个输入流，将 xml 文件加载到输入流中
			in = new FileInputStream("src/res/books.xml");
			InputStreamReader isr = new InputStreamReader(in, "UTF-8");
			//3.通过 saxBuilder 的 build 方法，将输入流加载到 saxBuilder 中
			Document document = saxBuilder.build(isr);
			//4.通过 document 对象获取 xml 文件的根节点
			Element rootElement = document.getRootElement();
			//5.获取根节点下的子节点的 List 集合
			List<Element> bookList = rootElement.getChildren();
			
			//继续进行解析
			for(Element book: bookList){
				Book bookEntity = new Book();
				System.out.println("---开始解析第"+ (bookList.indexOf(book)+1) +"本书---");
				//解析 book 的属性集合
				List<Attribute> attrList = book.getAttributes();
				//知道节点下属性名称时，获取属性值：book.getAttributeValue("id");
				//遍历 attrList（不清楚 book 节点下属性的名字及数量时）
				for(Attribute attr: attrList){
					//获取属性名
					String attrName = attr.getName();
					//获取属性值
					String attrValue = attr.getValue();
					System.out.println("属性名："+ attrName +"---属性值："+ attrValue);
					if(attrName.equals("id")){
						bookEntity.setId(attrValue);
					}
				}
				
				//对 book 节点的子节点的节点名以及节点值的遍历
				List<Element> bookChilds = book.getChildren();
				for(Element child: bookChilds){
					System.out.println("节点名："+ child.getName() +"---节点值："+ child.getValue());
					if(child.getName().equals("name")){
						bookEntity.setName(child.getValue());
					}
					else if(child.getName().equals("author")){
						bookEntity.setAuthor(child.getValue());
					}
					else if(child.getName().equals("year")){
						bookEntity.setYear(child.getValue());
					}
				}
				System.out.println("---结束解析第"+ (bookList.indexOf(book)+1) +"本书---");
				booksList.add(bookEntity);
				bookEntity = null;
				System.out.println(booksList.size());
				System.out.println(booksList.get(0).getId());
				System.out.println(booksList.get(0).getName());
			}
			
		} catch//略
```

### 4-6 关于 JDOM 使用过程中 JAR 包的引用

前面我们添加 jar 包的时候是选择 添加到外部归档 ，这样其实并没有真正把 jar 包导入到项目中，所以在项目迁移中会出现问题，接下来说下如何导入 jar 包的到项目中。

1. 首先将之前添加的 jar 包 remove 掉；

2. 新建一个 lib 文件夹，放入要导入的 jdom jar 包；

3. 当前项目， 选择 构建路径 -> 配置构建路径 -> 库 -> 添加JAR包，选择 lib 文件夹中的 jdom jar 包；

这样就导入完成了，此时可以看到 workspace 中有一个 lib 文件夹，里边放有刚刚导入的 jar 包。

### 4-7 应用 DOM4J 解析节点属性

* 先导入 DOM4J 的 jar 包

``` java
//解析 books.xml 文件
//创建 SAXReader 的对象 reader
SAXReader reader = new SAXReader();
//通过 reader 对象的 read 方法加载 books.xml 文件
Document document = reader.read(new File("src/res/books.xml"));
//通过 document 对象获取根节点 bookStore
Element bookStore = document.getRootElement();
Iterator it = bookStore.elementIterator();
//遍历迭代器，获取根节点中的信息
while(it.hasNext()){
	System.out.println("---开始遍历---");
	Element book = (Element) it.next();
	//获取 book 的属性名以及属性值
	List<Attribute> bookAttrs = book.attributes();
	for(Attribute attr: bookAttrs){
		System.out.println("属性名："+ attr.getName() +" ---属性值："+ attr.getValue());
		
	}
	System.out.println("---结束遍历---");
}
```

### 4-8 应用 DOM4J 解析子节点的信息
``` java
	Iterator itt = book.elementIterator();
	while(itt.hasNext()){
		Element bookChild = (Element) itt.next();
		System.out.println("节点名："+ bookChild.getName()+"---节点值："+ bookChild.getStringValue());
	}
```


## 第5章 四种 XML 解析方式大 PK

### 5-1 四种解析方式的分析

#### DOM 与 SAX

**DOM 解析的优缺点：**

优点：
* 形成了树结构，直观好理解，代码更易编写
* 解析过程中树结构保留在内存中，方便修改

缺点：
* 当 xml 文件较大时，对内存耗费比较大，容易影响解析性能并造成内存溢出

**SAX 解析的优缺点：**

优点：
* 采用事件驱动模式，对内存耗费比较小
* 适用于只需要处理 xml 中数据时

缺点：
* 不易编码
* 很难同时访问同一个 xml 中的多处不同数据

#### JDOM 与 DOM 、 DOM4J

 **JDOM** 
* 仅适用具体类而不适用接口
*  API 大量使用了 Collections 类

 **DOM4J** 
*  JDOM 的一种智能分支，合并了许多超出基本 XML 文档表示的功能
*  DOM4J 使用接口和抽象基本类方法，是一个优秀的 Java XML API
* 具有性能优异、灵活性好、功能强大和极端易使用的特点

### 5-2 四种解析方式解析速度分析

JUnit 是 Java 提供的用来进行单元测试的自动化工具

如何在项目同添加 JUnit 支持：当前项目，选择 构建路径 -> 添加库 -> JUnit ，选择最新版本 JUnit 4 ，添加完成

现在只需要在单元测试的方法前面加上 `@Test` 就可以使用了，并且测试方法可以写在任意类的任意位置中

