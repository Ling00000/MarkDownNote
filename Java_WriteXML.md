title : 结合 Java 程序的 XML（二）
date  : 2017/5/16

---

# 文件写入

## 第1章 简介

## 第2章 通过 DOM 方式生成 XML 文档

### 2-1 创建根节点和 book 节点属性

### 2-2 创建 XML 文件

### 2-3 生成节点间的文本
``` java
public class DOMTest {
	
	public DocumentBuilder getDocumentBuilder(){
		// 创建一个 DocumentBuilderFactory 的对象
		DocumentBuilderFactory dbf = DocumentBuilderFactory.newInstance();
		//创建 DocumentBuilder 对象
		DocumentBuilder db = null;
		try {
			db = dbf.newDocumentBuilder();
		} catch (ParserConfigurationException e) {
			// TODO 自动生成的 catch 块
			e.printStackTrace();
		}
		return db;
	}
	
	/**
	 * DOM 解析 xml 文件
	 */
	public void xmlParser() {...
	}

	/**
	 * DOM 生成 xml 文件
	 */
	public void xmlCreate(){
		DocumentBuilder db = getDocumentBuilder();
		Document document = db.newDocument();
		Element bookstore = document.createElement("bookStore");
		//向 bookstore 根节点中添加子节点 book
		Element book = document.createElement("book");
		Element name = document.createElement("name");
		name.setTextContent("第一本书");
		book.appendChild(name);
		book.setAttribute("id", "1");
		//将 book 节点添加到 bookstore 根节点中
		bookstore.appendChild(book);
		//将已经包含了book 的 bookstore 节点添加到 dom 树中
		document.appendChild(bookstore);
		
		//创建 TransformerFactory 对象
		TransformerFactory tff = TransformerFactory.newInstance();
		try {
			//创建 Transformer 对象
			Transformer tf = tff.newTransformer();
			//进行合理换行
			tf.setOutputProperty(OutputKeys.INDENT, "yes");
			//生成文件
			tf.transform(new DOMSource(document), new StreamResult(new File("books1.xml")));
		} catch (...) {...
		}
	}

	public static void main(String[] args) {
		//创建 DOMTest 对象
		DOMTest test = new DOMTest();
		//调用解析方法，解析 xml 文件
//		test.xmlParser();
		test.xmlCreate();
	} 
}
```

## 第3章 通过 SAX 方式生成 XML 文档

### 3-1 SAX 生成 XML 的准备工作
``` java
/**
    * SAX 生成 xml 文件
    * @param args
    */
public void xmlCreate(){
	ArrayList<Book> bookList = xmlParser();
	//生成 xml
	//1.创建一个 TransformerFactory 类的对象
	SAXTransformerFactory tff = (SAXTransformerFactory) SAXTransformerFactory.newInstance();
	try {
		//2.通过 SAXTransformerFactory 对象创建一个 TransformerHandler 对象
		TransformerHandler handler =  tff.newTransformerHandler();
		//3.通过 handler 对象创建一个 Transformer 对象
		Transformer tr = handler.getTransformer();
		//4.通过 Transformer 对象对生成的 xml 文件进行设置
		//4.1 设置 xml 的编码
		tr.setOutputProperty(OutputKeys.ENCODING, "UTF-8");
		//4.2 设置 xml 的换行
		tr.setOutputProperty(OutputKeys.INDENT, "yes");
		//5.创建 Result 对象
		File f = new File("src/res/books2.xml");
		if(!f.exists()){
			f.createNewFile();
		}
		//6.创建 Result 对象，并且使其与 handler 关联
		Result result = new StreamResult(new FileOutputStream(f));
		//注意1：Transformer 设置文件只有在调用 setResult() 前才能生效
		//注意2：setResult() 在调用 startDocument() 之前
		handler.setResult(result);
    } catch (...) {...
    }
}
```

### 3-2 生成子节点及节点属性
``` java
		//7.利用 handler 对象进行 xml 文件内容的编写
		//打开 document
		handler.startDocument();
		AttributesImpl attr = new AttributesImpl();
		handler.startElement("", "", "bookstore", attr);
		attr.clear();
		attr.addAttribute("", "", "id", "", "1");
		handler.startElement("", "", "book", attr);
		handler.endElement("", "", "book");
		handler.endElement("", "", "bookstore");
		//关闭 document
		handler.endDocument();
```

### 3-3 生成带文本的子节点
``` java
		//7.利用 handler 对象进行 xml 文件内容的编写
		//打开 document
		handler.startDocument();
		AttributesImpl attr = new AttributesImpl();
		handler.startElement("", "", "bookstore", attr);
		for(Book book: bookList){
			attr.clear();
			attr.addAttribute("", "", "id", "", book.getId());
			handler.startElement("", "", "book", attr);
			//创建 name 节点
			if(book.getName() != null && !book.getName().trim().equals("")){
				attr.clear();
				handler.startElement("", "", "name", attr);
				handler.characters(book.getName().toCharArray(), 0, book.getName().length());
				handler.endElement("", "", "name");					
			}
			//创建 year 节点
			if(book.getYear() != null && !book.getYear().trim().equals("")){
				attr.clear();
				handler.startElement("", "", "year", attr);
				handler.characters(book.getYear().toCharArray(), 0, book.getYear().length());
				handler.endElement("", "", "year");
			}
			//创建 author 节点
			if(book.getAuthor() != null && !book.getAuthor().trim().equals("")){
				attr.clear();
				handler.startElement("", "", "author", attr);
				handler.characters(book.getAuthor().toCharArray(), 0, book.getAuthor().length());
				handler.endElement("", "", "author");
			}
			handler.endElement("", "", "book");
		}
		handler.endElement("", "", "bookstore");
		//关闭 document
		handler.endDocument();
```

## 第4章 通过 DOM4J 方式生成 XML 文档

### 4-1 什么是 RSS

RSS 通常是用来描述和同步网站内容的一种格式，本质是 xml ，这也符合了 xml 存在的目的 —— xml 通常的用途就是用来共享数据

### 4-2 生成 RSS 根节点及 version 属性
``` java
public void xmlCreate(){
	//1.创建 document 对象，代表整个 xml 文档
	Document document = DocumentHelper .createDocument();
	//2.创建根节点
	Element rss = document.addElement("rss");
	//3.向 rss 节点中添加 version属性
	rss.addAttribute("version", "2.0");
	//6.生成 xml 文件
	File file = new File("rssnews.xml");
	XMLWriter writer;
	try {
		writer = new XMLWriter(new FileOutputStream(file));
		writer.write(document);
		writer.close();
	} catch (IOException e) {
		// TODO 自动生成的 catch 块
		e.printStackTrace();
	}
}
```

### 4-3 生成子节点和内容并设置换行
``` java
	//3.向 rss 节点中添加 version属性
	//4.生成子节点及节点内容
	Element channel = rss.addElement("channel");
	Element title = channel.addElement("title");
	title.setText("国内最新新闻");
	//5.设置生成 xml 的格式
	OutputFormat format = OutputFormat.createPrettyPrint();
	format.setEncoding("GBK");
	//6.生成 xml 文件
```

### 4-4 处理转义字符
``` java
	title.setText("<![CDATA[警惕网络病毒“走进新时代”]]>");

	//设置是否转义，默认值是 true ，代表转义
	writer.setEscapeText(false);	
```

## 第5章 通过 JDOM 方式生成 XML 文档

### 5-1 JDOM 生成 XML 根节点
``` java
public void xmlCreate(){
	//1.生成一个根节点
	Element rss = new Element("rss");
	//2.为节点添加属性
	rss.setAttribute("version", "2.0");
	//3.生成一个 document 对象
	Document document = new Document(rss);
	//4.创建 XMLOutputter 对象
	XMLOutputter outputer = new XMLOutputter();
	//5.利用 outputer 将 document 对象转换成 xml 文档
	try {
		outputer.output(document, new FileOutputStream(new File("rssnews1.xml")));
	} catch (...) {...
	}
}
```

### 5-2 JDOM 添加子节点及节点间文本
``` java
	//3.生成一个 document 对象
		
	Element channel = new Element("channel");
	rss.addContent(channel);
	Element title = new Element("title");
	title.setText("国内最新新闻");
	channel.addContent(title);
	
	//4.创建 XMLOutputter 对象
```
关于转义字符的处理：
``` java
	Element title = new Element("title");
	CDATA cdata = new CDATA("<!警惕网络病毒“走进新时代”>");
	title.addContent(cdata);
	channel.addContent(title);
```

### 5-3 JDOM 设置 XML 格式
``` java
	//Format format = Format.getCompactFormat();
	//format.setIndent("");
	//上边两行代码等效为下边一行代码
	Format format = Format.getPrettyFormat();
	format.setEncoding("GBK");
	//4.创建 XMLOutputter 对象
	XMLOutputter outputer = new XMLOutputter(format);
```

## 第6章 不同生成方法大 PK

### 6-1 四种写入方式理论对比

DOM --> 基于树结构

SAX --> 基于事件

DOM4J、JDOM --> 基于底层 API

**DOM 与 SAX**

* DOM ：生成的 DOM 树会驻留在内存中，这样的好处是便于后续随时的删除修改和重新排列等改动

* SAX ：性能高但是不方便修改

### 6-2 四种写入方式性能代码对比
