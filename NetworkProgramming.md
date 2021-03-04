## 端口

端口表示计算机上的一个程序的进程：

* 不同的进程有不同的端口号，用来区分软件

* 0~65535

* 分为TCP端口、UDP端口

* 端口分类

  * 公有端口 0~1023

    - HTTP: 80
    - HTTPS: 443
    - FTP: 21
    - Telent: 23

  * 程序注册端口：1024~49151

    * Tomcat: 8080
    * MySQL: 3306
    * Oracle: 1521

  * 动态、私有：49152~65535

    ```bash
    netstat -ano #查看所有端口
    netstat -ano|findstr "5353"
    ```

    

## Java的两个类

* InetAddress

```java
import java.net.InetAddress;
import java.net.UnknownHostException;

//测试IP
public class TestInetAddress {
    public static void main(String[] args) {
        try {
            //查询网站ip地址
            InetAddress byName = InetAddress.getByName("www.baidu.com");
            System.out.println(byName);

            //本机ip
            InetAddress local = InetAddress.getLocalHost();
            System.out.println(local);

            //常用方法
            //System.out.println(byName.getAddress());
            //System.out.println(byName.getCanonicalHostName());
            System.out.println(byName.getHostAddress()); //ip
            System.out.println(byName.getHostName());  //域名
        } catch (UnknownHostException e) {
            e.printStackTrace();
        }
    }
}

```

* InetSocketAddress

```java
import java.net.InetSocketAddress;

public class TestInetSocketAddress {
    public static void main(String[] args) {
        InetSocketAddress socketAddress = new InetSocketAddress("127.0.0.1", 8080);
        System.out.println(socketAddress);

        System.out.println(socketAddress.getAddress());
        System.out.println(socketAddress.getHostName());
        System.out.println(socketAddress.getPort());
    }
}
```



## TCP/UDP

TCP:连接 打电话

* 连接，稳定

* **三次握手**、**四次挥手**

  ```
  最少三次 保证稳定连接
  A: 你瞅啥?
  B: 瞅你咋地?
  A: 干一场!
  
  最少四次 断开
  A:我要走了！
  B:你真的要走了吗？
  B:你真的真的要走了吗？
  A:我真的真的要走了
  ```

  

* 分为客户端、服务端

* 传输完成才释放连接

UDP:不连接 发短信

* 不连接 不稳定
* 客户端服务端之间没有明确的界限
* 不管有没有准备好 都可以发给你



## TCP代码示例

**服务端：**

1. 建立服务的端口 ServerSocket
2. 等待用户的连接 serverSocket.accept()
3. 接收消息

* TcpServer.java:

```java
import java.io.ByteArrayOutputStream;
import java.io.InputStream;
import java.net.ServerSocket;
import java.net.Socket;

//服务器
public class TcpServer {
    public static void main(String[] args) {
        try {
            //占用进程地址
            ServerSocket serverSocket = new ServerSocket(9999);
            //等待连接
            Socket socket = serverSocket.accept();
            //读取消息
            InputStream is = socket.getInputStream();

            //管道流
            ByteArrayOutputStream bas = new ByteArrayOutputStream();
            byte[] buffer = new byte[1024];
            int len;
            while ((len = is.read(buffer)) != -1) {
                bas.write(buffer, 0, len);
            }

            System.out.println(bas.toString());

            serverSocket.close();
            socket.close();
            is.close();
            bas.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

**客户端：**

1. 连接服务器 Socket
2. 发送消息

* TcpClient.java

```java
import java.io.IOException;
import java.io.OutputStream;
import java.net.InetAddress;
import java.net.Socket;
import java.nio.charset.StandardCharsets;

//客户端
public class TcpClient {
    public static void main(String[] args) throws IOException {
        try {
            // 地址 端口号
            String ip = "127.0.0.1";
            int port = 9999;
            // socket连接
            Socket socket = new Socket(ip, port);
            // 发送信息 IO流
            OutputStream os = socket.getOutputStream();
            os.write("你好，我是奥特曼".getBytes(StandardCharsets.UTF_8));

            os.close();
            socket.close();


        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```

