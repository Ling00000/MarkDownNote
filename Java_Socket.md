title : Java 中的网络编程—— Socket 通信
date  : 2017/5/18

---

# 第1章 网络基础知识 

## 1-1 网络基础 

### 两台计算机通过网络进行通信要满足的条件

1. 唯一的标识：IP 地址
2. 共同的语言：协议
3. 区分不同应用程序的通信：端口号

### TCP/IP 协议

1. 目前世界上应用最为广泛的协议
2. 以 TCP（Transmission Control Protocol ，传输控制协议）和 IP（Internet Protocol ，互联网协议）为基础的不同层次上多个协议的集合
3. 位于 TCP/IP 模型的第四层——传输层


### IP 地址

1. 为实现网络中不同计算机之间的通信，每个机器的唯一标识，类似于手机号码
2. IP 地址格式：数字型，如：192.168.0.1（使用较多的IPv4版本，定义了长度为32位二进制）

### 端口

1. 用来区分不同的应用程序
2. 端口号范围为 0 ~ 65535 ，其中 0 ~ 1023 为系统所保留
3. IP 地址和端口号组成了 Socket ， Socket 是网络上运行的程序之间双向通信链路的终结点，是 TCP 和 UDP 的基础
4. 常用的端口号：http：80，ftp：21，telnet：23

### Java 中的网络支持

针对网络通信的不同层次，Java 提供的网络功能有四大类：

1. InetAddress ：用于标识网络上的硬件资源
2. URL ：统一资源定位符，通过 URL 可以直接读取或写入网络上的数据
3. Sockets ：使用 TCP 协议实现网络通信的 Socket 相关的类
4. Datagram ：使用 UDP 协议，将数据保存在数据报中，通过网络进行通信


# 第2章 Java 中网络相关 API 的应用 

## 2-1 Java 中的 InetAddress 的应用

InetAddress 类用于标识网络上的硬件资源，表示互联网协议（IP）地址。

``` java
//获取本机的 InetAddress 实例
InetAddress address = InetAddress.getLocalHost();
System.out.println("计算机名：" + address.getHostName());
System.out.println("IP 地址：" + address.getHostAddress());
//获取字节数组形式的 IP 地址
byte[] bytes = address.getAddress();
System.out.println("字节数组形式的 IP ："+Arrays.toString(bytes));
//直接输出 InetAddress 对象
System.out.println(address);

//根据机器名获取 InetAddress 实例
InetAddress address2 = InetAddress.getByName("pc");
System.out.println("计算机名：" + address2.getHostName());
System.out.println("IP 地址：" + address2.getHostAddress());

//根据 IP 地址获取 InetAddress 实例
InetAddress address3 = InetAddress.getByName("192.168.1.227");
System.out.println("计算机名：" + address3.getHostName());
System.out.println("IP 地址：" + address3.getHostAddress());
```

## 2-2 Java 中的 URL 的应用

### URL 

1. URL（Uniform Resource Locator）统一资源定位符，表示 Internet 上某一资源的地址
2. URL 由两部分组成：协议名称和资源名称，中间用冒号隔开，如： http://www.baidu.com
3. 在 java.net 包中，提供了 URL 类来表示 URL

```java
//创建一个 URL 实例
URL imooc = new URL("http://www.imooc.com");
//?后面表示参数，#后面表示锚点
URL url = new URL(imooc, "/index.html?username=tom#test");
System.out.println("协议："+url.getProtocol());
System.out.println("主机："+url.getHost());
//如果未指定端口号，则使用默认端口号，此时 getPort() 方法返回值为-1
System.out.println("端口："+url.getPort());
System.out.println("文件路径："+url.getPath());
System.out.println("文件名："+url.getFile());
System.out.println("相对路径："+url.getRef());
System.out.println("查询字符串："+url.getQuery());
```

### 使用 URL 读取网页内容

1. 通过 URL 对象的 `openStream()` 方法可以得到指定资源的输入流
2. 通过输入可以读取、访问网络上的数据

``` java
//创建一个 URL 实例
URL url = new URL("http://www.baidu.com");
//通过 URL 的 openStream 方法获取 URL 对象所表示的资源的字节输入流
InputStream is = url.openStream();
//将字节输入流转换为字符输入流
InputStreamReader isr = new InputStreamReader(is, "UTF-8");
//为字符输入流添加缓冲
BufferedReader br = new BufferedReader(isr);
//读取数据
String data = br.readLine();
while(data!=null){
    //输出数据
    System.out.println(data);
    data = br.readLine();
}
br.close();
isr.close();
is.close();
```

# 第3章 通过 Socket 实现 TCP 编程 

## 3-1 Socket 简介

### Socket 通信
1. TCP 协议是面向连接、可靠的、有序的，以字节流的方式发送数据
2. 基于 TCP 协议实现网络通信的类：客户端的 Socket 类，服务器端的 SeverSocket 类

### Socket 通信模型

1. 服务端建立倾听 socket 
2. 客户端创建连接 socket，向服务端发送请求 
3. 服务端等待并接收连接请求 
4. 建立连接 
5. 用 InputStream 和 OutputStream 进行通信 
6. 关闭两端 socket 及相关资源 
7. 结束通信 

### Socket 通信实现步骤
1. 创建 ServerSocket 和 Socket
2. 打开连接到 Socket 的输入输出流
3. 按照协议对 Socket 进行读写操作
4. 关闭输入输出流、关闭 Socket

## 3-2 编程实现基于 TCP 的 Socket 通信之服务器端

## 3-3 编程实现基于 TCP 的 Socket 通信之客户端

## 3-4 完善用户登陆之服务器响应客户端

### 服务器端

1. 创建 ServerSocket 对象，绑定监听端口
2. 通过 `accept()` 方法监听客户端请求
3. 连接建立后，通过输入流读取客户端发送的请求信息
4. 通过输出流向客户端发送响应
5. 关闭相关资源，如输入输出流、Socket等

``` java
/*
 * 基于 TCP 协议的 Socket 通信，实现用户登录
 * 服务器端
 */
public class Server {
	public static void main(String[] args) {
		try {
			//1.创建一个服务器端 Socket ，即 ServerSocket ，指定绑定的端口，并监听此端口
			ServerSocket serverSocket = new ServerSocket(8888);
			//2.调用 accept() 方法开始监听，等待客户端的连接
			System.out.println("***服务器即将启动，等待客户端的连接***");
			Socket socket = serverSocket.accept();
			//3.获取输入流，并读取客户端信息
			//3.1 字节输入流
			InputStream is = socket.getInputStream();
			//3.2 字节流转换为字符流
			InputStreamReader isr = new InputStreamReader(is);
			//3.3 为输入流添加缓冲
			BufferedReader br = new BufferedReader(isr);
			String info = null;
			//3.4 循环读取客户端信息
			while((info=br.readLine()) != null){
				System.out.println("我是服务器，客户端说：" + info);
			}
			//3.5 关闭输入流
			socket.shutdownInput();
			//4.获取输出流，响应客户端的请求
			OutputStream os = socket.getOutputStream();
			//4.1 包装为打印流
			PrintWriter pw = new PrintWriter(os);
			pw.write("欢迎您！");
			//4.2 调用 flush() 方法将缓冲输出
			pw.flush();
			//5.关闭资源
			pw.close();
			os.close();
			br.close();
			isr.close();
			is.close();
			socket.close();
			serverSocket.close();
		} catch (IOException e) {
			e.printStackTrace();
		}
	}
}
```

### 客户端

1. 创建 Socket 对象，指明需要连接的服务器的地址和端口号
2. 连接建立后，通过输出流向服务器端发送请求信息
3. 通过输入流获取服务器响应的信息
4. 关闭相关资源

``` java
/*
 * 客户端
 */
public class Client {
	public static void main(String[] args) {
		try {
			//1.创建客户端 Socket ，指定服务器地址和端口
			Socket socket = new Socket("localhost", 8888);
			//2.获取输出流，向服务器端发送信息
			//2.1 字节输出流
			OutputStream os = socket.getOutputStream();
			//2.2 将输出流包装为打印流
			PrintWriter pw = new PrintWriter(os);
			pw.write("用户名：admin;密码：123");
			pw.flush();
			//2.3关闭输出流
			socket.shutdownOutput();
			//3.获取输入流，并读取服务器端的响应信息
			InputStream is = socket.getInputStream();
			BufferedReader br = new BufferedReader(new InputStreamReader(is));
			String info = null;
			while((info=br.readLine()) != null){
				System.out.println("我是客户端，服务器说：" + info);
			}
			//4.关闭资源
			br.close();
			is.close();
			pw.close();
			os.close();
			socket.close();
		} catch (UnknownHostException e) {
			e.printStackTrace();
		} catch (IOException e) {
			e.printStackTrace();
		}
	}
}
```
* 注意运行时要先运行服务器端然后再运行客户端，可以在服务器端控制台看到服务器端已经接收到客户端发送的信息

## 3-5 使用多线程实现多客户端的通信

多线程服务器：应用多线程来实现服务器与多客户端之间的通信

基本步骤
1. 服务端创建 ServerSocket ，循环调用 accept() 等待客户端连接
2. 客户端创建一个 socket 并请求和服务器端连接
3. 服务器端接受客户端请求，创建 socket 与该客户建立专线连接
4. 建立连接的两个 socket 在一个单独的线程上对话
5. 服务器端继续等待新的连接

``` java
/*
 * 服务器端线程处理类
 */
public class ServerThread extends Thread {
	//和本线程相关的 Socket
	Socket socket = null;
	public ServerThread(Socket socket){
		this.socket = socket;
	}
	
	//线程执行的操作，响应客户端的请求
	public void run(){
		InputStream is = null;
		InputStreamReader isr = null;
		BufferedReader br = null;
		OutputStream os = null;
		PrintWriter pw = null;
		try {
			//获取输入流，并读取客户端信息
			is = socket.getInputStream();
			isr = new InputStreamReader(is);
			br = new BufferedReader(isr);
			String info = null;
			while((info=br.readLine()) != null){
				System.out.println("我是服务器，客户端说：" + info);
			}
			//关闭输入流
			socket.shutdownInput();
			//获取输出流，响应客户端的请求
			os = socket.getOutputStream();
			pw = new PrintWriter(os);
			pw.write("欢迎您！");
			//调用 flush() 方法将缓冲输出
			pw.flush();
		} catch (IOException e) {
			e.printStackTrace();
		} finally{
			//关闭资源
			try {
				if(pw!=null)
					pw.close();
				if(os!=null)
					os.close();
				if(br!=null)
					br.close();
				if(isr!=null)
					isr.close();
				if(is!=null)
					is.close();
				if(socket!=null)
					socket.close();
			} catch (IOException e) {
				e.printStackTrace();
			}
		}
	}
}
```

``` java
/*
 * 服务器端
 */
public class Server {
	public static void main(String[] args) {
		try {
			//创建一个服务器端 Socket ，即 ServerSocket ，指定绑定的端口，并监听此端口
			ServerSocket serverSocket = new ServerSocket(8888);
			Socket socket = null;
			//记录客户端的数量
			int count = 0;
			System.out.println("***服务器即将启动，等待客户端的连接***");
			//循环监听等待客户端的连接
			while(true){
				//调用 accept() 方法开始监听，等待客户端的连接
				socket = serverSocket.accept();
				//创建一个新的线程
				ServerThread severThread = new ServerThread(socket);
				//启动线程
				severThread.start();
				//统计客户端的数量
				count ++;
				System.out.println("客户端的数量："+count);
				InetAddress address = socket.getInetAddress();
				System.out.println("当前客户端的 IP ："+address.getHostAddress());
			}
			
		} catch (IOException e) {
			e.printStackTrace();
		}
	}
}
```

# 第4章 通过 Socket 实现 UDP 编程 

## 4-1 DatagramPacket

### UDP 协议（用户数据报协议）
1. 是无连接、不可靠的、无序的
2. 以数据报作为数据传输的载体
3. 进行数据传输时，首先需要将要传输的数据定义成数据报（Datagram），在数据报中指明数据所要达到的 Socket（主机地址和端口号），然后再将数据报发送出去

### 相关操作类：
1. `DatagramPacket` ：表示数据报包
2. `DatagramSocket` ：进行端到端通信的类

## 4-2 编程实现基于 UDP 的 Socket 通信之服务器端

## 4-3 编程实现基于 UDP 的 Socket 通信之客户端

### 服务器端

1. 创建 DatagramSocket ，指定端口号
2. 创建 DatagramPacket
3. 接收客户端发送的数据信息
4. 读取数据

``` java
/*
 * 实现基于 UDP 的用户登录
 * 服务器端
 */
public class UDPServer {
	public static void main(String[] args) throws IOException {
		/*
		 * 接收客户端发送的数据
		 */
		//1.创建服务器端 DatagramSocket，指定端口
		DatagramSocket socket = new DatagramSocket(8800);
		//2.创建数据报，用于接收客户端发送的数据
		byte[] data = new byte[1024];
		DatagramPacket packet = new DatagramPacket(data, data.length);
		//3.接收客户端发送的数据
		System.out.println("***服务器端已启动，等待客户端发送数据");
		//此方法在接收到数据报之前会一直阻塞
		socket.receive(packet);
		//4.读取数据
		String info = new String(data, 0, packet.getLength());
		System.out.println("我是服务器，客户端说："+info);
		/*
		 * 向客户端响应数据
		 */
		//1.定义客户端的地址、端口号、数据
		InetAddress address = packet.getAddress();
		int port = packet.getPort();
		byte[] data2 = "欢迎您！".getBytes();
		//2.创建数据报，包含响应的数据信息
		DatagramPacket packet2 = new DatagramPacket(data2, data2.length, address, port);
		//3.响应客户端	
		socket.send(packet2);
		//4.关闭资源
		socket.close();
	}
}
```

### 客户端

1. 定义发送的数据信息，如地址、端口号等
2. 创建 DatagramPacket ，包含将要发送的信息
3. 创建 DatagramSocket
4. 发送数据

``` java
/*
 * 客户端
 */
public class UDPClient {
	public static void main(String[] args) throws IOException {
		/*
		 * 向服务器端发送数据
		 */
		//1.定义服务器的地址、端口号、数据
		InetAddress address = InetAddress.getByName("localhost");
		int port = 8800;
		byte[] data = "用户名：admin；密码：123".getBytes();
		//2.创建数据报，包含发送的数据信息
		DatagramPacket packet = new DatagramPacket(data, data.length, address, port);
		//3.创建 DatagramSocket 对象
		DatagramSocket socket = new DatagramSocket();
		//4.向服务器端发送数据报
		socket.send(packet);
		/*
		 * 接收服务器端响应的数据
		 */
		//1.创建数据报，用于接收服务器端响应的数据
		byte[] data2 = new byte[1024];
		DatagramPacket packet2 = new DatagramPacket(data2, data2.length);
		//2.接收服务器响应的数据
		socket.receive(packet2);
		//3.读取数据
		String reply = new String(data2, 0, packet2.getLength());
		System.out.println("我是客户端，服务器说："+reply);
		//4.关闭资源
		socket.close();
	}
}
```

# 第5章 Socket 总结 

## 5-1 Socket 总结

### 重点
1. Socket 通信原理
2. 基于 TCP 的 Socket 通信

### 经验和技巧
1. 多线程的优先级：未设置优先级可能会导致运行时速度非常慢，可降低优先级
2. 是否关闭输入输出流：对于同一个 socket ，如果关闭了输出流，则与该输出流关联的 socket 也会被关闭，所以一般不用关闭流，直接关闭 socket 即可
3. 使用 TCP 通信传输对象
4. socket 编程传递文件

# 第6章 综合练习 

## 6-1 综合练习---问题描述

## 6-2 综合练习---实现分析
